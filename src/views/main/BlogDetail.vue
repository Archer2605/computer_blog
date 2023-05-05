<template>
    <div v-if="blog_detail" class="col-lg-9" >
        <div class="row">
            <div class="blog_detail_img">
                <img v-if="blog_detail.image"
                    :src="'http://localhost:3000/images/' + blog_detail.image"
                    alt=""
                    />
            </div>
            <h5 class="blog_detail_name"> {{ blog_detail.title }} </h5>
            <br>
            <div class="blog_detail_content">
                <p>{{ blog_detail.header }}
                </p>
                <p class="blog_detail_content_sub">{{ blog_detail.body }}
                </p>
                <p>{{ blog_detail.footer }}
                </p>
            </div>
            <div class="w-100">
                <p><span class="font-weight-bold mr-3">Category:    </span>{{ blog_detail.category}}</p>
            </div>
            <div style="margin-bottom:100px;" class="form-group w-100">
                <!-- <h5>Comment</h5>
                    <textarea class="form-control" id="exampleFormControlTextarea1" rows="3"></textarea>
                    <button class="btn2 text-center btn_review btn-primary">Submit</button> -->
                <div  class="row d-flex justify-content-center">
                    <div class="col">
                        <div class="card shadow-0 border">
                            <div class="card-body p-4">
                                <div v-if="isAuthentication" class="form-outline mb-4">
                                    <input v-model="content_comment" type="text" id="addANote" class="form-control" placeholder="Comment..." />
                                    <label v-if="info_updata.status_update" @click="handlerUpdateComment()" class="form-label" for="addANote">
                                    <button type="button" class="btn btn-primary">
                                        Updated
                                    </button></label>
                                    <label v-else @click="handlerSubmitComment()" class="form-label" for="addANote">
                                        <button type="button" class="btn btn-primary">
                                            Send
                                        </button>
                                    </label>
                                </div>
                                <div v-for="comment in blog_detail.comment" :key="comment._id" class="card mb-4">
                                    <div class="card-body p-3">
                                        <div class="d-flex justify-content-between">
                                            <h5 class="mb-2 ms-2">{{ comment.username }}</h5>
                                            <div v-if="comment.username == username_current">
                                                <span @click="handlerClickUpdate(comment._id, comment.content)" class="badge badge-secondary" style="cursor:pointer"><i class="fa-solid fa-pen"></i></span>
                                                <span @click="handlerCliCkDeleteComment(comment._id)" class="badge badge-danger ml-2" style="cursor:pointer"><i class="fa-solid fa-trash"></i></span>
                                            </div>
                                        </div>
                                        <p>{{ comment.content }}</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <h1 v-else>Loading...</h1>
</template>
<script>
    import store from '@/store';
    // import { mapActions } from 'vuex';
    import axios from 'axios'
    export default{
        data(){
           return {
                blog_detail: {
                    title: "",
                    category: "",
                    header: "",
                    body: "",
                    footer: "",
                    image: ""
                },
                content_comment:"",
                info_updata: {
                    status_update: false,
                    id_comment: ""
                }
           }
        },
        computed:{
            isAuthentication(){
                return store.state.auth.isAuthentication
            },
            username_current(){
                return store.state.auth.username
            }
        },
        methods: {
            handlerSubmitComment(){
                const data = {
                    username : store.state.auth.username,
                    content : this.content_comment 
                }

                // alert(data.username)

                const id = this.$route.params.id;
                axios.post('http://localhost:3000/api/blog/comment/'+id, data)
                    .then(response=>{
                        if(response.status == 200){
                            this.content_comment = ""
                            axios.get('http://localhost:3000/api/blog/'+id)
                            .then(response => {
                                if(response.status == 200){
                                    this.blog_detail = response.data
                                }
                            })
                            .catch(()=>{
                                console.log("Loi created")
                            })
                        }
                    })
                    .catch(error=>{
                        console.log(error)
                    })
    
            },
            handlerCliCkDeleteComment(id){
            const id_blog = this.$route.params.id;
            const id_comment = id
                axios.delete('http://localhost:3000/api/blog/comment/'+id_blog+'?id_comment='+id_comment)
                .then(response=>{
                    if(response.status == 200){
                        axios.get('http://localhost:3000/api/blog/'+id_blog)
                            .then(response => {
                                if(response.status == 200){
                                    this.blog_detail = response.data
                                }
                            })
                            .catch(()=>{
                                console.log("Loi created")
                            })
                    }
                })
                .catch(error=>{
                    console.log(error)
                })
            },
            handlerClickUpdate(id,content){
                this.info_updata.status_update = true
                this.info_updata.id_comment = id
                
                this.content_comment = content
            },
            handlerUpdateComment(){
                const id_blog = this.$route.params.id;
                const id_comment = this.info_updata.id_comment
                const data = {
                    id: id_comment,
                    content: this.content_comment
                }
                console.log(id_blog, id_comment)
                axios.put('http://localhost:3000/api/blog/comment/'+id_blog,data)
                    .then(response=>{
                    if(response.status == 200){
                        this.content_comment = ""
                        axios.get('http://localhost:3000/api/blog/'+id_blog)
                            .then(response => {
                                if(response.status == 200){
                                    this.blog_detail = response.data
                                }
                            })
                            .catch(()=>{
                                console.log("Loi created")
                            })
                    }
                    })
                    .catch(error=>{
                        console.log(error)
                    })
            }
        },
        created(){
            const id = this.$route.params.id
            axios.get('http://localhost:3000/api/blog/'+id)
                .then(response => {
                    if(response.status == 200){
                        this.blog_detail = response.data
                    }
                })
                .catch(()=>{
                    console.log("Loi created")
                })
        },
        updated(){
            const id = this.$route.params.id
            axios.get('http://localhost:3000/api/blog/'+id)
                .then(response => {
                    if(response.status == 200){
                        this.blog_detail.title = response.data.title
                        this.blog_detail.image = response.data.image
                        this.blog_detail.header = response.data.header
                        this.blog_detail.body = response.data.body
                        this.blog_detail.footer = response.data.footer
                        this.blog_detail.category = response.data.category
                    }
                })
                .catch(()=>{
                    console.log("Loi created")
                })
        }
    }
</script>
<style></style>