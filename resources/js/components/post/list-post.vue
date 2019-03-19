<template>
    <div class="container">
        <div class="col-md-12">
            <div class="row">
                <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#post">
                    Add New
                </button>
            </div>
        </div>
        <table class="table table-hover">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Title</th>
                    <th>Content</th>
                    <th>Date</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(post, id) in posts" :key="id">
                    <td>{{ post.id }}</td>
                    <td>{{ post.title }}</td>
                    <td>{{ post.content }}</td>
                    <td>{{ post.created_at }}</td>
                    <td>
                        <button type="button" class="btn btn-success" @click="editPost(post.id)">Edit</button>
                    </td>
                </tr>
            </tbody>
        </table>
       <!--  Create-post -->
        <div class="modal fade" id="post">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                        <h4 class="modal-title">Modal title</h4>
                    </div>
                    <div class="modal-body">
                        <div class="form-group">
                            <label for="">Title</label>
                            <input type="text" class="form-control" id="" placeholder="Input field" v-model="title">
                        </div>
                        <div class="form-group">
                            <label for="">Content</label>
                            <input type="text" class="form-control" id="" placeholder="Input field" v-model="content">
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="submit" class="btn btn-primary" @click="savePost" data-dismiss="modal">Submit</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {

  name: 'list-post',

  data () {
        return {
            posts: [],
            title:'',
            content:''
        }
    },
    methods : {
        getAllPost () {
            window.axios.get(route('post.index')).then(res => {
                this.posts = res.data;
            })
        },
        savePost () {
            let self = this;
            window.axios.post(route('post.store',{
                'title': this.title,
                'content': this.content
            })).then(res => { 
                self.title = res.data.title;
                self.content = res.data.content;
            })
        },
        editPost (id) {
            let self = this;
                $('#post').modal('show');
                // window.axios.post(route('post.edit',{
                //     'id': id,chmo
                // })).then(res => { 
                //     self.title = res.data.title;
                //     self.content = res.data.content;
                // })
        }
    },
    created () {

    },
    mounted () {
        this.getAllPost();
    }
}
</script>

<style lang="css" scoped>
</style>
