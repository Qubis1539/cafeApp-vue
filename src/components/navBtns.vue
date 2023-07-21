<template>
    <div class="buttons">
        <!-- :class="[randomPressed ? 'active': '']" -->
        <div class="btn active" @click="resetClick"  >
            <img src="@/assets/Reset.svg" alt="">
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
        gap: 5px;
    }
    
    .btn{
       
        width: 70px;
        height: 70px;   
        display: flex;
        justify-content: center;
        align-items: center;
        background: #e5e5e5;
        border-radius: 50%;
        cursor: pointer;
        transition: background .2s, top .6s;
        position: relative;
        z-index: 5;
        
    }
    .btn:first-child{
        top: 60px;
        z-index: 4;
        width: 50px;
        height: 50px;
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