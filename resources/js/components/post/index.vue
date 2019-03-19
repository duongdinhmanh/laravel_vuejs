<template>
    <div>
        <list-post></list-post>
    </div>
</template>

<script>
import ListPost from '../post/list-post';

export default {

    name: 'index',
    components: {
        'list-post': ListPost,
    },
    data () {
        return {

        }
    }
}
</script>

<style lang="css" scoped>
</style>
