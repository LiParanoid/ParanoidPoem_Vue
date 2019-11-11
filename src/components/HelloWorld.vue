<template>
    <el-row>
        <el-col :span="8">
            <el-image style="width: 200px; height: 200px" :src="src">
            </el-image>
        </el-col>
        <el-col :span="8">
            <el-carousel :interval="4000" type="card" height="200px">
                <el-carousel-item v-for="item in 6" :key="item">
                    <h3 class="medium">{{ item }}</h3>
                </el-carousel-item>
            </el-carousel>
        </el-col>
        <el-col :span="8">
            <div class="grid-content bg-purple"></div>
        </el-col>
    </el-row>

</template>

<script>
    export default {
        name: 'HelloWorld',
        data () {
            return {
                value: new Date(),
                msg: 'Welcome to Your Vue.js App',
                showMsg: '点我获取数据',
                happyValue: 50,
                src: require('../assets/head.jpg')
            }
        },
        methods: {
            getInfo: function () {
                var that = this;
                that.$http({
                    method: 'GET',
                    url: 'api/hello' //this指data
                }).then(response => {
                    alert(JSON.stringify(response));
                    that.showMsg = response["data"];
                }).catch(function (error) {
                    console.log(error)
                })
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .el-carousel__item h3 {
        color: #475669;
        font-size: 14px;
        opacity: 0.75;
        line-height: 200px;
        margin: 0;
    }

    .el-carousel__item:nth-child(2n) {
        background-color: #99a9bf;
    }

    .el-carousel__item:nth-child(2n + 1) {
        background-color: #d3dce6;
    }
</style>
