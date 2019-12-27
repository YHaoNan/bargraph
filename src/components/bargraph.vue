<template>
    <div class="bar-graph">
        <div class="bar-graph-title">
            {{title}}
        </div>
        <div class="bar-graph-container">

            <div class="bar-graph-episode">
                {{currentItem.episode}}
            </div>

            <transition-group appear>
                <Bar :key="item.name" v-for=" item in currentData" :index="currentIndex" :title="item.name" :num="item.num" :max="currentData[0].num" :color="getColor(item.name)"></Bar>
            </transition-group>
        </div>
    </div>
</template>

<script>
    import Bar from './bar'
    import { randomColor16 } from '../utils'
    let colorMap = {}
    export default {
        name: "bargraph",
        components: {
            Bar,
        },
        props: {
            datas : {
                required: true,
            },
            intervalToNext : {
                required: true,
                type: Number
            },
            title: {
                required: true,
                type: String,
                default: "Bar Graph"
            }
        },
        data () {
            return {
                currentItem: [],
                currentIndex: 0
            }
        },
        computed: {
            currentData: function () {
                if (this.currentItem["datas"]){
                    var tempList = this.currentItem["datas"]
                    return tempList.sort((a,b)=>b["num"]-a["num"])
                }
                return this.currentItem["datas"]
            }
        },
        methods: {
            start: function () {
                let that = this
                let interval = setInterval(function () {
                    if (that.currentIndex == that.datas.length){
                        clearInterval(interval)
                        interval = null
                    }
                    that.currentItem = that.datas[that.currentIndex++]
                },this.intervalToNext)
            },
            getColor: function (name) {
                if (!colorMap.hasOwnProperty(name))
                    colorMap[name] = randomColor16()
                return colorMap[name]
            }
        },
        mounted() {
            this.start();
        }
    }
</script>

<style scoped>
    .bar-graph-title{
        font-weight: bold;
        font-size: 2em;
        margin-bottom: 1em;
    }
    .bar-graph-container{
        position: relative;
        text-align: left;
    }

    .bar-graph-episode{
        font-weight: bold;
        font-size: 2em;
        position: absolute;
        bottom: 0;
        right: 0;
    }
    .v-enter, .v-leave-to {
        opacity: 0;
        transform: translateY(50px);
    }

    .v-enter-active, .v-leave-active{
        transition: all ,0.2s;
    }
    .v-move{
        transition: all 0.2s;
    }
    .v-leave-active{
        position: absolute;
    }
</style>
