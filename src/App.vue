<template>
    <div id="app">
        <h2>Add new counter</h2>
        <h1 v-if="error">{{msg}}</h1>
        <label>Value</label>
        <input type="text" v-model="value">
        <label>Format size</label>
        <input type="text" v-model="format">
        <button class="addCounter" @click="addCounter">Add!</button>
        <counter v-for="counter in counters"
                     :value="counter.value"
                     :format="counter.format"
                     :id="counter.id"
                     :key="counter.id"
                     @remove="removeCounter">
        </counter>
    </div>
</template>

<script>
import scoreCounter from './components/scoreCounter.vue'

export default {
    name:'app',
    data () {
        return {
            value:0,
            format:1,
            msg:"Try again, wrong format",
            error:false,
            counters:[
                {
                    value:3,
                    format:4,
                    id: Math.random()
                },
                {
                    value:5,
                    format:2,
                    id: Math.random()
                },
                {
                    value:10,
                    format:3,
                    id: Math.random()
                }
            ],
        }
    },
    components:{
        'counter': scoreCounter
    },
    methods:{
        addCounter(){
            if(this.checkLength() === false){

                this.error=false
                this.counters.push({
                value: this.value,
                format: this.format,
                id: Math.random()
                })
            }else{
                this.error=true
            }
        },
        removeCounter(index){
            return this.counters = this.counters.filter(el => el.id != index )
        },
        checkLength(){
            return this.value.toString().length > this.format
        }
    }
}
</script>

<style>
    body{
        margin:0;
        padding:0;
        background-color:lightgrey;
    }
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        flex-direction:column;
        display:flex;
        justify-content: center;
        align-items: center;
        color: #2c3e50;
    }
    .addCounter{
        margin:15px;
        padding:5px 15px;
        background-color:#3F51B5;
        border:0;
        border-radius:2px;
        height:30px;
        width:100px;
        text-align:center;
        color:#fff;
    }
    label{
        font:18px 'arial',sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }
    h1, h2 {
        font-weight: normal;
    }
</style>
