<template>
    <div class="app">
        <cafeList>

        </cafeList>
        
    </div>
</template>

<script>
    import cafeList from '@/components/cafeList.vue';
    


    export default{
        components:{
            cafeList,
           
        },
        data(){
            return{
                cafes: []
            }
        },
        methods:{
            async getData() {
            const res = await fetch("https://bandaumnikov.ru/api/test/site/get-index");
            const finalRes = await res.json();
            this.cafes = finalRes.data;
            console.log(finalRes);
        }
        },
        mounted() {
            this.getData();
        }
        
    }
    
</script>


<style>

</style>