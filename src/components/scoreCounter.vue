<template>
    <transition name="counter">
        <div id="wrapper">
            <h1>Counter :<span>{{formattedValue()}}</span></h1>
            <button class="increment" @click="increment">+</button>
            <button class="decrement" @click="decrement">-</button>
            <input type="text" v-model="newValue"/>
            <button class="setValue" @click="setValue">Set</button>
            <button class="resetValue" @click="reset">Reset</button>
            <button class="deleteCounter" @click="remove">Delete</button>
        </div>
    </transition>
</template>

<script>
export default{
       data(){
            return{
                actualValue:this.value,
                actualFormat:this.format,
                index:this.id,
                newValue:0
            }
       },
       props:["value","format","id"],
       methods:{
            increment(){
                if(this.actualValue < Math.pow(10,this.actualFormat)-1){
                    this.actualValue++
                }
            },
            decrement(){
                if(this.actualValue > 0){
                    this.actualValue--
                }
            },
            setValue(){
                if(this.newValue <= Math.pow(10,this.actualFormat)-1 & this.newValue > 0)
                    this.actualValue = this.newValue
            },
            reset(){
                this.actualValue = 0
            },
            formattedValue(){
                return Array(this.actualFormat - this.actualValue.toString().length+1).join('0') + this.actualValue
            },
            remove(){
                this.$emit('remove',[this.index])
            }
        }
}
</script>

<style>
    @keyframes fadeOut{
        0%{
            transform:scale(1);
        }
        50%{
            transform:scale(1.1);
        }
        100%{
            transform:scale(0);
        }
    }
    #wrapper{
        background-color:#673AB7;
        padding:20px 35px;
        margin: 15px 0;
        border-radius:5px;
        -webkit-box-shadow:0px 0px 10px #757575;
    }
    .counter-leave-active{
        animation:fadeOut 1s;
    }
    .increment,.decrement{
        background-color:#673AB7;
        font:20px 'arial',sans-serif;
        border:0;
        text-align:center;
        color:#fff;
    }
    .setValue,.resetValue{
        background-color:#2E7D32;
        border:0;
        border-radius:2px;
        height:24px;
        text-align:center;
        color:#fff;
    }
    .deleteCounter{
        background-color:#F44336;
        border:0;
        border-radius:2px;
        height:24px;
        text-align:center;
        color:#fff;
    }
    h1{
        color:#fff;
        font:40px 'arial',sans-serif;
        text-align:center;
    }
    input{
        margin:0 5px;
        width:100px;
        height:20px;
        border-radius:3px;
        border:0;
    }
</style>