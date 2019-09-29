<template>
<v-container>
  <v-layout row wrap>
    <v-flex xs12 text-xs-center>
      <h1>TODO List</h1>
      <p>전체 할 일 : {{ todoList.length }}/ 완료된 할 일 : {{ countDone }}/ 남은 할 일: {{todoList.length - countDone}}</p>
    </v-flex>
    <v-flex xs6 pa-2>
      <List :todoList="todoList"
            @statusControl = "statusControl" @listDelete = "listDelete"/>
    </v-flex>
    <v-flex xs6 pa-2>
      <ListAdd @listAdd="listAdd" @listEdit="listEdit"/>
    </v-flex>
  </v-layout>
</v-container>
</template>

<script>
import List from './List' // 리스트를 보여줄 컴포넌트
import ListAdd from './ListAdd' // 리스트를 더 해줄 컴포넌트

export default {
  components:{
    List,
    ListAdd
  },
  data() {
    return {
      todoList: []
    }
  },
  methods:{
    listAdd(memo){
      console.log('받았어!');
      this.todoList.push({ memo: memo, status: 'created' });
    },
    statusControl(index, status){
      this.todoList[index].status = status
    },
    listDelete(index){
      this.todoList.splice(index, 1)
    },
    listEdit(memo, index){
      this.todoList[index].memo = memo
    }
  },
  computed:{
    countDone(){
        let count = 0;
        this.todoList.forEach(list => {
          if(list.status === 'done'){
            count ++
          }
        })
        return count
    }
  }
}
</script>