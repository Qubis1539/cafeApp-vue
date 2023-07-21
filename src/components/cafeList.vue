<template>
    <div class="cafesList" >
        <div class="cafeItem" v-for="cafe in allCafes" :key="cafe.id">
            <div class="cafeItem__top">
                <img v-if="cafe.photo" :src="cafe.photo" alt="" class="cafeItem__img">
                <img v-else  src="http://chudo-prirody.com/uploads/posts/2021-08/1628905019_37-p-skachat-foto-milikh-kotikov-41.jpg" alt="" class="cafeItem__img">
                <h2 class="cafeItem__title">{{ cafe.name }} <a :href="'https://t.me/share/url?url='+curUrl+'?id='+cafe.id+'&text='+msgText + cafe.name" target="_blank"><img src="@/assets/Share.svg" class="cafeItem__share"></a></h2>
                <div class="cafeItem__cuisine">
                    <div v-if="cafe.cuisine">Тип кухни: {{cafe.cuisine}}</div>
                    <div v-else>N/D</div>
                </div>
            </div>
            
            <div class="cafeItem__info">
                <div class="cafeItem__address cafeItem__flex">
                    <span class="classItem__ico">
                        <img src="@/assets/PlaceMarker.svg" alt="">
                    </span>
                    <span v-if="cafe.address" >{{  cafe.address  }}</span>
                    <span v-else>N/D</span>
                </div>
                
                <div class="cafeItem__landMark cafeItem__flex">
                    <span v-if="cafe.landmark">{{ cafe.landmark }}</span>
                    <span v-else>N/D</span>
                </div>
                <div class="cafeItem__distance cafeItem__flex">
                    <span class="classItem__ico">
                        <img src="@/assets/distance.png" alt="">
                    </span>
                    <span v-if="cafe.distance">
                        {{ cafe.distance }}м
                    </span>
                    <span v-if="cafe.distance && cafe.time"> / </span>
                    <span v-if="cafe.time">
                        {{cafe.time}}мин
                    </span>
                    <span v-if="!cafe.distance && !cafe.time">N/D</span>
                </div>
                <div class="cafeItem__price cafeItem__flex">
                    <span class="classItem__ico">
                        <img src="@/assets/DollarCoin.svg" alt="">
                    </span>
                    <span v-if="cafe.price">{{ cafe.price }}</span> 
                    <span v-else>N/D</span>
                </div>
                <img v-if="cafe.business_lunch" src="@/assets/businesslunch.png" alt="" class="cafeItem__businessLunch">
                <!-- <div class="cafeItem__share">
                    d
                    <q-btn>
                        <ShareNetwork
                            network="facebook"
                            url="https://news.vuejs.org/issues/180"
                            title="Say hi to Vite! A brand new, extremely fast development setup for Vue."
                            description="This week, I’d like to introduce you to 'Vite', which means 'Fast'. It’s a brand new development setup created by Evan You."
                            quote="The hot reload is so fast it\'s near instant. - Evan You"
                            hashtags="vuejs,vite"
                        >
                            Share on Facebook
                        </ShareNetwork>
                    </q-btn>
                </div> -->

            </div>
        </div>

    </div>
    <navBtns @randEl="randEl" @resEl="resEl">

    </navBtns>
</template>

<script>
import navBtns from "@/components/navBtns.vue";
    export default{
        components:{
            navBtns,
        },
        
        data(){
            return{
                cafes: [],
                allCafes: [],
                curUrl: window.location.origin,
                msgText: "Привет, гляди какое место нашел! Кафе "
            }
            
        },
        methods:{
            getUrlParameter(sParam) {
                let sPageURL = window.location.search.substring(1),
                    sURLVariables = sPageURL.split('&'),
                    sParameterName,
                    i;

                for (i = 0; i < sURLVariables.length; i++) {
                    sParameterName = sURLVariables[i].split('=');

                    if (sParameterName[0] === sParam) {
                        return sParameterName[1] === undefined ? true : decodeURIComponent(sParameterName[1]);
                    }
                }
                return false;
            },
            async getData() {
                let id = this.getUrlParameter("id");
                let url ="https://bandaumnikov.ru/api/test/site/get-index"
                const res = await fetch(url);
                const finalRes = await res.json();
                this.cafes = finalRes.data;
                this.allCafes = this.cafes;

                if (id){
                    this.randEl(id)
                }
                
            

            },
           randEl(n = undefined) {
            if (n == undefined){
                n = Math.round(Math.random() * (this.cafes.length - 1));
            }
            this.allCafes = [this.cafes[n]];
           },
           resEl() {
            this.allCafes = this.cafes
           }
        },
       mounted() {
            this.getData()
       },
        
        
    }
</script>

<style>
:root{
    --main-color: #C37A44;
}
.cafesList{

    
    margin: 0 auto;
    max-width: 1400px;
    
    display: grid; 
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    grid-template-rows: 1fr 1fr 1fr 1fr 1fr repeat(1fr, 20); 
    grid-auto-flow: row;
    gap: 40px; 
    
}
.cafeItem__flex{
    display: flex;
    align-items: start;
}
.cafeItem{
    position: relative;
    background: #dedede;
    padding-bottom: 20px;

}
.cafeItem__top{
    position: relative;
    height: 250px;
}
.cafeItem__img{
    width: 100%;
    object-fit: cover;
    height: 250px;
}
.cafeItem__title{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    text-align: center;
    color: white;
    background: #0000009c;
    padding: 10px 0;
}
.cafeItem__title h2{
    position: relative;
}
.cafeItem__info{
    
    padding:10px 20px;
    padding-top: 15px;
}
.cafeItem__distance{
    justify-content: end;
    text-align: right;
}
.cafeItem__price{
    font-weight: bold;
    color: var(--main-color);
    font-size: 22px;
}
.classItem__ico{
    margin-right: 4px;
}
.cafeItem__landMark{
    font-size: 14px;
    margin-bottom: 16px;
}
.cafeItem__cuisine{
    position: absolute;
    bottom: 0;
    left: 0;
    text-align: center;
    width: 100%;
}
.cafeItem__cuisine div{
    width: 100%;
    color: white;
    background: #0000009c;
    padding: 5px 0;
    
}
.cafeItem__businessLunch{
    position: absolute;
    right: 20px;
    bottom: 0px;
}
.cafeItem__share{
    position: absolute;
    right: 10px;
    cursor: pointer;
}
</style>