<template>
    <div class="buttons">
        <!-- :class="[randomPressed ? 'active': '']" -->
        <div class="btn active" @click="resetClick"  >
            <img src="@/assets/refresh.svg" alt="">
        </div>
        <div class="btn" @click="randClick">
            <img src="@/assets/Dice.svg" alt="">
        </div>
        
    </div>
</template>

<script>
export default {
    props:{
            cafes:{
                tyoe: Array,
                required: true
            },
            
        },
    data(){
            return{
                randomPressed: false,
            }
        },
        methods:{
            randClick(){
                this.randomPressed = true;
                this.$emit("randEl")
            },
            resetClick(){
                this.randomPressed = false;
                this.$emit("resEl")
            }
        },
        mounted() {
            
        }
}
</script>

<style>
    .buttons{
        position: fixed;
        right: 20px;
        bottom: 30px;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 5px;z-index: 100;
    }
    
    .btn{
       
        width: 56px;
        height: 56px;   
        display: flex;
        justify-content: center;
        align-items: center;
        background: #44B3C2;
        filter: drop-shadow(0px 0px 0px rgba(0, 0, 0, 0.10)) drop-shadow(0px 2px 4px rgba(0, 0, 0, 0.10)) drop-shadow(0px 7px 7px rgba(0, 0, 0, 0.09)) drop-shadow(0px 16px 9px rgba(0, 0, 0, 0.05)) drop-shadow(0px 28px 11px rgba(0, 0, 0, 0.01)) drop-shadow(0px 44px 12px rgba(0, 0, 0, 0.00));
        border-radius: 50%;
        cursor: pointer;
        transition: background .2s, top .6s;
        position: relative;
        z-index: 100;
        
    }
    .btn:first-child{
        top: 60px;
        width: 34px;
        height: 34px;
    }
    .btn.active{
        top: 0;
    }
    .btn img{
        min-width: 2    0px;
        width: 71%;
        transition: all .8s;
    }
    .btn:active{
        background: #c2c2c2;
    }
    .btn:hover img{
        transform: rotate(360deg);
    }
    
</style>