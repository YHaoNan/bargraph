<template>
    <div class="bar" :ref="title + '-outer'" >
        <span class="bar-title" >
            {{title}} {{num+suffix}}
        </span>
        <canvas class="bar-canvas" :ref="title" :width="barWidth - 120" height="20">

        </canvas>
    </div>
</template>

<script>

    export default {
        name: "bar",
        props: {
            index: {
                required: true,
                type: Number
            },
            num: {
                required: true,
                type: Number
            },
            max: {
                required: true,
                type: Number
            },
            color: {
                required: true,
                type: String
            },
            title: {
                require: true,
                type: String
            },
            suffix: {
                required: false,
                default: "%"
            }
        },
        data (){
            return {
                barWidth: 0,
            }
        },
        watch:{
            index () {
                this.barWidth = this.bar.clientWidth
                var ctx=this.canvas.getContext("2d");
                ctx.fillStyle = this.color
                let rectWidth = (this.num / this.max) * this.barWidth
                ctx.clearRect(0,0,this.barWidth,20)
                ctx.fillRect(0,0,rectWidth,20)
            },
        },
        computed: {
            bar : function (){return this.$refs[this.title+"-outer"]},
            canvas: function (){return this.$refs[this.title]}
        },
        mounted () {
        }
    }
</script>

<style scoped>
    .bar{
        margin-top: 5px;
        width: 100%;

    }
    .bar-title{
        display: inline-block;
        width: 100px;
        text-align: right;
    }
    .bar-canvas{
        margin-left: 20px;
    }


</style>
