<template>
    <div class="root">
        <span>书签分类</span>
        <ul>
            <li></li>
        </ul>
    </div>
</template>
<script>

    import {getSortApi} from '../utils/api'

    export default {
        data() {
            return {
                a: 'aaa'
            }
        },
        mounted() {
            this.getSort()
            console.log('query-sort',this.getSort())

        },
        methods:{
            getSort(){ getSortApi().then(res=>{console.log(res)}) }
        }


    }
</script>
<style lang="scss">
    .root {
        font-size: 20px;

        > .left-list {
            width: 2rem;

        }
    }


</style>
