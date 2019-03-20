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
                        <button type="button" class="btn btn-success" @click="editPostId(post.id)">
                                Edit
                        </button>
                    </td>
                </tr>
            </tbody>
        </table>
        
            <div class="modal hide fade edit-post" tabindex="-1" role="dialog" id="post">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h4 class="modal-title">Modal title</h4>
                        </div>
                        <div class="modal-body">
                            <div class="form-group">
                                <label for="">Title</label>
                                <input type="text" class="form-control" id="" placeholder="Input field" v-model="data.title">
                            </div>
                            <div class="form-group">
                                <label for="">Content</label>
                                <input type="text" class="form-control" id="" placeholder="Input field" v-model="data.content">
                            </div>
                        </div>
                        <div class="modal-footer" v-if="isId === true">
                            <button type="submit" class="btn btn-primary" @click="saveEditPost" data-dismiss="modal">Submit</button>
                        </div>
                        <div class="modal-footer" v-else>
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
            data: {
                title:'',
                content:'',
            },
            isId: false,
            idPost: null,
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
                this.getAllPost();
            })
        },
        editPostId (id) {
            this.idPost = id;
            window.$('#post').modal('show');
            let self = this;
            window.axios.get(route('post.edit',{'id': id
            })).then(res => {
               self.data = res.data;
               self.isId = true
            })
        },
        saveEditPost () {
            const headers = {
                'Content-Type': 'multipart/form-data'
            };
            let param = this.data;
            let self = this;
            window.axios.put(route('post.update', {id: this.idPost }),{param}).then(res => {
                window.$('#post').modal('hide');
                self.getAllPost();
            })
        },
    },
    mounted () {
        this.getAllPost();
    }
}
</script>

<style lang="css" scoped>
</style>
