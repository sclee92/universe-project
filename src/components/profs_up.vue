<template>
    <div id="profs_up" class="main">
        <div class="update_form">
            <h1>교수 정보 수정</h1>
            <div v-for="item in prof" :key="item.prof_id">
                <label>이름</label>
                <input type="text" v-model="item.prof_name">
                <label>나이</label>
                <input type="text" v-model="item.prof_age">
            </div>
            <label>학과</label>
            <select v-model="sub">
                <option value="" selected hidden>학과 정보를 선택하세요</option>
                <option v-for="item in this.$store.state.subjects" :key="item.subject_id" :value="item.subject_name">{{item.subject_name}}</option>
            </select>
            <div class="update_btns">
                <button @click="updateData">등록</button>
                <button class="back" @click="$router.go(-1)">돌아가기</button>
            </div>
        </div>
    </div>
</template>

<script>

import axios from 'axios';
axios.defaults.baseURL = 'http://172.16.28.165:8889';

export default{
    name:'profs_up',
    data(){
        return{
            id : this.$route.params.ids,
            sub : "",
            prof : []
        }
    },
    methods:{
        getData(){
            axios.get('/getProfAll/' + this.id)
            .then((res)=>{
                this.prof = res.data
            })
            .catch((err)=>{
                console.log(err);
            })
        },
        updateData(){
            axios.put('/', {
                prof_id : this.id,
                prof_name : this.name,
                prof_age : this.age,
                prof_subject : this.sub
            })
            .then((res)=>{
                console.log(res);
            })
            .catch((err)=>{
                console.log(err);
            })
            console.log(this.sub)
        }  
    },
    created(){
        this.getData();
    }
}
</script>