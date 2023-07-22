<template>
    <div class="cafesList" >
        <div class="cafeItem" v-for="cafe in allCafes" :key="cafe.id">
            <div class="cafeItem__top">
                <img v-if="cafe.photo" :src="cafe.photo" alt="" class="cafeItem__img">
                <img v-else  src="http://chudo-prirody.com/uploads/posts/2021-08/1628905019_37-p-skachat-foto-milikh-kotikov-41.jpg" alt="" class="cafeItem__img">
                
                <img v-if="cafe.business_lunch" src="@/assets/businesslunch.png" alt="" class="cafeItem__businessLunch">
            </div>
            
            <div class="cafeItem__info">
                <div class="cafeItem__header">
                    <a class="cafeItem__share" :href="'https://t.me/share/url?url='+curUrl+'?id='+cafe.id+'&text='+msgText + cafe.name" target="_blank"><img src="@/assets/Share.svg" class="cafeItem__share"></a>
                
                    <div class="cafeItem__cuisine">
                        <span v-if="cafe.cuisine">{{cafe.cuisine}} кухня</span>
                        <span v-else>N/D</span>
                    </div>
                    <h2 class="cafeItem__title">{{ cafe.name }} </h2>
                    <div class="cafeItem__landmark cafeItem__flex">
                        <span class="classItem__ico classItem__ico--address">
                            <img src="@/assets/message.svg" alt="">
                        </span>
                        <span v-if="cafe.landmark" >{{  cafe.landmark  }}</span>
                        <span v-else>N/D</span>
                    </div>
                    <div class="cafeItem__address cafeItem__flex">
                        <span class="classItem__ico classItem__ico--address">
                            <img src="@/assets/PlaceMarker.svg" alt="">
                        </span>
                        <span v-if="cafe.address" >{{  cafe.address  }}</span>
                        <span v-else>N/D</span>
                    </div>
                    <div class="cafeItem__distance cafeItem__flex">
                        <span class="classItem__ico">
                            <img src="@/assets/walk.svg" alt="">
                        </span>
                        <span v-if="cafe.distance">
                            {{ cafe.distance }} м
                        </span>
                        <span v-else>N/D м</span>
                        <div class="dot"></div>
                        <span v-if="cafe.time" >
                            {{cafe.time}} мин
                        </span>
                        <span v-else>N/D мин</span>
                        <span class="classItem__ico classItem__ico--ml">
                            <img src="@/assets/Taxi.png" alt="">
                        </span>
                    </div>
                    
                </div> 
                <div class="cafeItem__footer">
                    <button class="cafeItem__price cafeItem__flex">
                        
                        <span v-if="cafe.price">Забронировать от {{ cafe.price }} Руб.</span> 
                        <span v-else>N/D</span>
                    </button>
                </div>       
                
                
              
                
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
                curUrl: window.location.origin + window.location.pathname,
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
            this.allCafes = [this.cafes[n+1]];
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
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&family=Ubuntu:wght@400;500&display=swap');
:root{
    --main-color: #C37A44;
}
.cafesList{
    padding: 3px;
    font-family: 'Ubuntu', sans-serif!important;

    
    margin: 0 auto;
    max-width: 1400px;
    
    display: grid; 
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    grid-template-rows: 1fr 1fr 1fr 1fr 1fr repeat(1fr, 20); 
    grid-auto-flow: row;
    gap: 40px; 
    align-items: start;
    justify-items: center;
    
}
.dot{
    width: 4px;
    height: 4px;    
    border-radius: 50%;
    background: #000;
    margin-right: 5px;
    margin-left: 5px;
    margin-bottom: -3px;
}
.cafeItem__flex{
    display: flex;
    align-items: center;
}
.cafeItem{
    position: relative;
    border-radius: 35px;
    box-shadow: 0px 0px 0px 0px rgba(0, 0, 0, 0.05), 0px 2px 3px 0px rgba(0, 0, 0, 0.05), 0px 6px 6px 0px rgba(0, 0, 0, 0.04), 0px 14px 8px 0px rgba(0, 0, 0, 0.03), 0px 25px 10px 0px rgba(0, 0, 0, 0.01), 0px 39px 11px 0px rgba(0, 0, 0, 0.00);
    max-width: 370px;
    width: 100%;
    
}
.cafeItem__top{
    height: 250px;
    position: relative;
}
.cafeItem__businessLunch{
    position: absolute;
    right: 24px;top: 10px;
    z-index: 10;
}
.cafeItem__bottom{
    display: flex;
    justify-content: space-between;
}
.cafeItem__title{
    font-size: 26.4px;
    font-style: normal;
    font-weight: 400;
}
.cafeItem__img{
    
    width: 100%;
    object-fit: cover;
    border-radius: 35px 35px 0px 0px;
    height: 250px;
}
.cafeItem__top::after{
    content: "";
    position: absolute;
    display: block;
    border-radius: 35px 35px 0px 0px;
    width: 100%;
    height: 100%;
    z-index: 2;
    top: 0;
    left: 0;
    background: linear-gradient(180deg, rgba(0, 0, 0, 0.25) 0%, rgba(0, 0, 0, 0.00) 100%);

}
.cafeItem__info{
    padding: 20px 30px;
    position: relative;
    display: inline-flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    box-sizing: border-box;
    width: 100%;
    gap: 20px;
    
    
}
.cafeItem__header{
    position: relative;
    display: flex;
    flex-direction: column;
    gap:10px;
    width: 100%;
}
.cafeItem__footer{
    width: 100%;
}
.cafeItem__share{
    position: absolute;
    right: 0;
    top: 0;
}
.cafeItem__cuisine{
    background: #6BD9F1;
    border-radius: 46px;
    padding: 5px 15px;
    font-size: 12px;
    font-weight: 400;
    align-self: start;
    display: inline-block;
}
.classItem__ico{
    margin-right: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
}
.classItem__ico--address{
    margin-right: 10px;
}
.classItem__ico--ml{
    margin-left: 5px;
}
.cafeItem__price{
    justify-self: end;
    border: none;
    outline: none;
    border-radius: 42px;
    background: #C37A44;
    padding: 20px 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: #FFF;
    font-size: 14px;
    font-weight: 500;
    width: 100%;
}
</style>