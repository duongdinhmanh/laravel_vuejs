<template>
    <div class="container">
        <div class="form-group">
            <label for="">Title</label>
            <input type="text" class="form-control" id="" placeholder="Input field">
        </div>
        <div class="form-group">
            <label for="">Content</label>
            <input type="text" class="form-control" id="" placeholder="Input field">
        </div>
        <div class="form-group">
            <button type="submit" class="btn btn-primary" data-dismiss="modal">Submit</button>
        </div>
    </div>
</template>

<script>
export default {

  name: 'edit-post',

    data () {
        return {
            
        }
    },
    mounted () {
            // window.get(route('post.edit'))
            //     .then(function (resp) {
            //         app.company = resp.data;
            //     })
            //     .catch(function () {
            //         alert("Could not load your company")
            //     });
    }
}
</script>

<style lang="css" scoped>
</style>

