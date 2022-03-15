<template>
    <div id="subjects" class="main">
        <div>
            <ul class="lists tbody">
                <li v-for="item in this.$store.state.subjects" :key="item.id">
                    <p class="short">{{item.id}}</p>
                    <p>{{item.subjectName}}</p>
                    <div class="short">
                        <button @click="goSubUp(item.id)"><img src="../assets/img/edit.png" alt="수정"></button>
                        <input style="display:inline-block; margin:0" v-model="selectData" :value="item.id" type="checkbox">
                    </div>
                </li>
            </ul>
            <div class="update_btns">
                <button class="colorbtn" @click="toggle">등록</button>
                <button class="colorbtn" @click="deleteSub">선택 삭제</button>
            </div>
        </div>
        <div style="background-color:green; width:100px; height:100px">
            box
        </div>
        <subjectnew/>
    </div>
</template>


<script>

import subjectnew from '../components/subjects_new';
import axios from 'axios';
axios.defaults.baseURL = 'http://172.16.28.167:8084';

export default{
    name : 'subjects',
    data(){
        return{
            selectData : []
        }
    },
    components:{
        subjectnew
    },
    methods:{
        goSubUp(num){
            this.$router.push({
                name: 'subjects_up',
                params : {
                    ids : num
                }
            })
        },
        toggle(){
            this.$store.commit('toggle');
        },
        deleteSub(){
            axios.delete('/api/subjects/', {
                data:{
                    'subjects' : this.selectData
                }
            })
            .then((res)=>{
                console.log(res);
                this.$router.go();
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