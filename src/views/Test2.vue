<template>
    <div class="home-container">
        <Header/>
        <div class="body-container">
            <div class="panel-left">
                <div class="title">
                    <span>书签分类</span>
                    <span>新增分类</span>
                </div>
                <div class="sort-detail">
                    <ul>
                        <li v-for="item in sortData" :key="item.id">

                            {{item.sort_name}}
                            <img src="../assets/edit.png" alt="编辑">
                            <img src="../assets/delete.png" alt="删除">
                        </li>
                    </ul>
                </div>
            </div>
            <div class="panel-right">
                <List>
                    <ListItem>
                        <a href="#">www.baidu.com</a>
                        <template slot="action">
                            <li>
                                <a href="">Edit</a>
                            </li>
                            <li>
                                <a href="">More</a>
                            </li>
                        </template>
                    </ListItem>
                </List>
            </div>
        </div>
        <Footer/>
    </div>
</template>

<script>
    import Header from '@/components/Header'
    import Footer from '@/components/Footer'
    import {getSortApi} from '../utils/api'

    export default {
        name: 'Home',
        components: { Header, Footer
        },
        data() {
            return {
                sortData:[]

            }
        },
        computed: {},
        created() {},
        mounted() {
            this.getSortData()
        },
        methods: {
            getSortData(){
                getSortApi().then(res=>this.sortData = res.data)
            }



        }



    }
</script>

<style lang="scss" scoped>
    @import "./test.scss";
</style>
