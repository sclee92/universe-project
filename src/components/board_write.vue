<template>
    <div id="board_write" class="main">
        <div>
            <input type="text" placeholder="작성자" v-model="writter">
            <input type="date" v-model="date">
            <input class="title_input" type="text" placeholder="제목을 입력하세요." v-model="title">
        </div>
        <div class="contents">
            <textarea v-model="contents" placeholder="내용을 입력하세요."></textarea>
        </div>
        <div class="update_btns">
            <button class="colorbtn" @click="newContents">글쓰기</button>
            <button class="back colorbtn" @click="$router.go(-1)">돌아가기</button>
        </div>
    </div>
</template>

<style scoped>
</style>

<script>
import axios from 'axios';
axios.defaults.baseURL = 'http://172.16.28.165:8889';

export default{
    name: 'board_write',
    data(){
        return{
            title : "",
            writter : "",
            date : "",
            contents : ""
        }
    },
    methods:{
        newContents(){
            axios.post('/', {
                board_title : this.title,
                board_writter : this.writter,
                board_date : this.date,
                board_contents : this.contents,
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