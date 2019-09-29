<template>
    <div>
        <!-- 삭제하거나 수정할 때 어떤 것인지를 알기 위해 index 사용 pa === pading all mb === margin bottom -->
        <v-card class="pa-3 mb-3" :class="{'done': list.status === 'done'}" v-for="(list, index) in todoList" :key="index">
            <p>{{list.memo}}</p>
            <v-btn fab flat small color="green" @click="$emit('statusControl', index, 'done')" v-if="list.status === 'created'"><i class="fas fa-check"></i></v-btn>
            <v-btn fab flat small color="blue" @click="$emit('statusControl', index, 'created')" v-else><i class="fas fa-redo-alt"></i></v-btn>
            <v-btn fab flat small color="red" @click="$emit('listDelete', index)"><i class="fas fa-trash-alt"></i></v-btn>
            <v-btn fab flat small color="yellow" v-if="list.status === 'created'" @click="listEdit(list.memo, index)"><i class="fas fa-edit"></i></v-btn>
        </v-card>
    </div>
</template>

<script>
import { eventBus } from '../main'
export default {
    props: ['todoList'],

    data(){
        return{

        }
    },
    methods:{
        listEdit(memo, index){
            eventBus.listEdit(memo, index)
        }
    }
}
</script>

<style scoped>
.done{
    background-color: rgba(0,0,0,0.1);
}
.done p{
    text-decoration: line-through;
    color: rgba(0, 0, 0, 0,5)
}
</style>