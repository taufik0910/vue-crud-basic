<template id="post-delete">
    <div>
        <h3>Delete Post {{post.title}} </h3>
    <form v-on:submit.prevent="deletePost">
        <button type="submit" class="btn btn-sx btn-danger" name="button"> Delete</button>
        <router-link class="btn btn-sx btn-primary" v-bind:to="'/'">Back</router-link>

        
    </form>        
    </div>
    
</template>

<script>
    export default{
        data: function(){
            return {post:{body:'',title:''}}
        },

        created: function () {
        let uri ='http://localhost:8000/posts/'+this.$route.params.id+'/edit';
        Axios.get(uri).then((response)=>{
            this.post = response.data;
        });          
        },

        methods:{
            deletePost: function(){
                let uri ='http://localhost:8000/posts/'+this.$route.params.id;
                Axios.patch(uri, this.post).then((Response)=>{
                    this.$router.push({name:'Listposts'})
                })
            }
        }

    }
</script>