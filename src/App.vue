<template>
    <div id="app">
            <BarGraph id="graph" :interval-to-next="500" title="TIOBE 1997-2019" :datas="barGraphData"></BarGraph>
        <span>* 数据是随机生成的，并非真实的tiobe排行榜</span>
    </div>
</template>

<script>
    import BarGraph from '@/components/bargraph'
    import datas from './datas'

    export default {
        name: 'app',
        components: {
            BarGraph
        },
        data() {
            return {
                barGraphData: datas
            }
        },
        mounted() {
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    #graph {
        padding: 20px;
    }

</style>
