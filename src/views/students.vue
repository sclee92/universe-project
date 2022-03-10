<template>
    <div id="students" class="main">
        <div>
            <ul class="lists tbody">
                <li v-for="item in this.$store.state.students" :key="item.studentId">
                    <p class="short">{{item.studentId}}</p>
                    <p>{{item.studentName}}</p>
                    <p class="short">{{item.studentAge}}</p>
                    <p>{{item.studentAddress}}</p>
                    <p>{{item.studentSubject}}</p>
                    <div class="short">
                        <button @click="goStuUp(item.studentId)"><img src="../assets/img/edit.png" alt="수정"></button>
                        <button @click="deleteStu(item.subjectId)"><img src="../assets/img/remove.png" alt="삭제"></button>
                    </div>
                </li>
            </ul>
            <div class="update_btns">
                <button class="colorbtn" @click="toggle">등록</button>
            </div>
        </div>
        <studentnew/>
    </div>
</template>


<script>

import studentnew from '../components/students_new';
import axios from 'axios';
axios.defaults.baseURL = 'http://172.16.28.167:8084';

export default{
    name : 'students',
    data(){
        return{
        }
    },
    components:{
        studentnew
    },
    methods:{
        goStuUp(num){
            this.$router.push({
                name: 'students_up',
                params : {
                    ids : num
                }
            })
        },
        toggle(){
            this.$store.commit('toggle');
        },
        deleteStu(num){
            axios.delete('/api/students/' + num)
            .then((res)=>{
                console.log(res);
            })
            .catch((err)=>{
                alert(err)
            })
        }
    },
    created(){
        this.$store.dispatch('getAll');
        this.$store.commit('sortBoards');
    }
}
</script>