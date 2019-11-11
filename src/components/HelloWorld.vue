<template>
        <el-card class="box-card">
            <div slot="header" class="clearfix">
                <span class="touchleft">{{title}}</span>
                <el-button style="float: right; padding: 3px 0" @click="getRandItem" type="success">换一个</el-button>
            </div>
            <div v-for="o in info" :key="o" class="text item touchleft">{{o }}</div>
        </el-card>
</template>

<script>
export default {
    name: "HelloWorld",
    data() {
        return {
            value: new Date(),
            msg: "Welcome to Your Vue.js App",
            showMsg: "点我获取数据",
            happyValue: 50,
            src: require("../assets/head.jpg"),
            title: "",
            info:[]
        };
    },
    mounted(){
        this.getRandItem();
    },
    methods: {
        getInfo: function() {
            var that = this;
            that.$http({
                method: "GET",
                url: "api/index" //this指data
            })
                .then(response => {
                    alert(JSON.stringify(response));
                    that.showMsg = response["data"];
                })
                .catch(function(error) {
                    console.log(error);
                });
        },
        getRandItem:function(){
            var that = this;
            that.$http({
                method: "GET",
                url: "api/getRandItem" //this指data
            })
                .then(response => {
                    that.title = response["data"]["title"];
                    const infoStr = response["data"]["paragraphs"];
                    that.info = JSON.parse(infoStr);
                })
                .catch(function(error) {
                    console.log(error);
                });
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.text {
    font-size: 14px;
}

.item {
    margin-bottom: 18px;
}
.touchleft{
    text-align: left;
}

.clearfix:before,
.clearfix:after {
    display: table;
    content: "";
}
.clearfix:after {
    clear: both;
}

.box-card {
    width: 400px;
}
</style>
