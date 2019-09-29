<template>
    <div>
        
        <v-textarea outline v-model="memo" label="TODO List를 입력해주세요.">
        </v-textarea>
        
        <v-btn @click="listAdd" v-if="mode === 'add'">리스트 추가</v-btn>
        <v-btn @click="listEdit" v-else>리스트 수정</v-btn>
    </div>
</template>

<script>
import { eventBus } from "../main"
export default {
    data(){
        return{
            memo: null,
            index: null,
            mode : 'add'
        }
    },
    methods:{
        listAdd(){
            if(this.memo === null){
                alert('할 일을 입력해주세요.')
            } else {
                this.$emit('listAdd',this.memo)
                this.memo = null
            }
        },
        listEdit() {
            if(this.memo === null){
                alert('할 일을 입력해주세요.')
            } else {
                this.$emit('listEdit',this.memo, this.index)
                this.memo = null
                this.mode = 'add'
            }
        }
    },
    created(){
        eventBus.$on('listEdit',(memo, index)=> {
            this.memo = memo
            this.index = index
            this.mode = 'edit'
        })
    }
}
</script>