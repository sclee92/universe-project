<template>
    <div v-show="$store.state.modalOn" class="modal_wrapper">
        <div @click="toggle" class="modal_bg"></div>
        <div class="modal">
            <h1>학생 정보 신규 등록</h1>
            <input type="text" v-model="name" placeholder="이름">
            <input type="text" v-model="age" placeholder="나이">
            <input type="text" v-model="address" placeholder="주소">
            <select>
                <option value="" selected hidden>학과 / 지도교수</option>
                <option v-for="item in this.$store.state.profs" :key="item.prof_id" :value="item.prof_id">{{item.prof_subject}} : {{item.prof_name}} 교수</option>
            </select>
            <button class="colorbtn">등록</button>
        </div>
    </div>
</template>

<script>

import axios from 'axios';
axios.defaults.baseURL = 'http://172.16.28.165:8889';

export default{
    name: 'student_new',
    data(){
        return{
            name: "",
            age: "",
            address: ""
        }
    },
    methods:{
        toggle(){
            this.$store.commit('toggle');
        },
        newData(){
            axios.post('/', {
                student_name : this.name,
                student_age : this.age,
                student_address : this.address
            })
            .then((res)=>{
                console.log(res);
            })
            .catch((err)=>{
                console.log(err);
            })
        }
    }
}
</script>