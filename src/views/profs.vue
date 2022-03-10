<template>
    <div id="profs" class="main">
        <div>
            <ul class="lists tbody">
                <li v-for="item in this.$store.state.profs" :key="item.id">
                    <p class="short">{{item.id}}</p>
                    <p>{{item.professorName}}</p>
                    <p class="short">{{item.professorAge}}</p>
                    <p>{{item.subjectName}}</p>
                    <div class="short">
                        <button @click="goProfUp(item.id)"><img src="../assets/img/edit.png" alt="수정"></button>
                            <button @click="deleteProf(item.id)"><img src="../assets/img/remove.png" alt="삭제"></button>
                    </div>
                </li>
            </ul>
            <div class="update_btns">
                <button class="colorbtn" @click="toggle">등록</button>
            </div>
        </div>
        <profnew/>
    </div>
</template>


<script>

import profnew from '../components/profs_new';
import axios from 'axios';
axios.defaults.baseURL = 'http://172.16.28.167:8084';

export default{
    name : 'profs',
    data(){
        return{
        }
    },
    components:{
        profnew
    },
    methods:{
        goProfUp(num){
            this.$router.push({
                name: 'profs_up',
                params : {
                    ids : num
                }
            })
        },
        toggle(){
            this.$store.commit('toggle');
        },
        deleteProf(num){
            axios.delete('/api/profs/' + num)
            .then((res)=>{
                console.log(res);
            })
            .catch((err)=>{
                console.log(err);
                alert('외부 등록된 항목 : 삭제할 수 없습니다.');
            })
        }
    },
    created(){
        this.$store.dispatch('getAll');
    }
}
</script>