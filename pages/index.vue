<template>
  <div class="container-fluid p-0" style="position:relative">
      <swiper  class="medium-plus-screens"  :options="swiperOption">
              <swiper-slide v-for="j in this.noumberOfSliders(apiData) " :key="j" style="left:-60px"> 
                    <div class="mt-5 ml-2 mr-0 row">           
                           <div v-for="i in articles[j-1].length" :key="i" class=" col-md m-1 p-0">
                                  <card  :title="articles[j-1][i-1].title" :description="articles[j-1][i-1].snippet" :image="articles[j-1][i-1].image" ></card>                                 
                           </div>            
                    </div>
              </swiper-slide> 
              <div class="swiper-button-prev mt-1" slot="button-prev"></div>
              <div class="swiper-button-next mt-1" slot="button-next"></div>             
      </swiper>
      
      <div class="small-screens">
            <div class="row mt-5 ml-2 mr-3">           
                  <div v-for="i in apiData.length - 1" :key="i" class="col-12 m-1 p-0">
                        <card  :title="apiData[i].title" :description="apiData[i].snippet" :image="apiData[i].image" ></card>                                 
                  </div>            
            </div>
      </div> 
  </div> 
</template>

<script>
  import card from "../components/card";  
  const axios = require('axios'); 

  export default {    
    async  asyncData(){         
        try{        
          const response = await axios.get("https://fuckup.gr/api/articles?fbclid=IwAR3Ba-dxX-z3JtS73IefQ6jbLjPECA2BcaRZ0gwVZZYqEArWJ10OxR10CkA"); 
          var apiData = response.data;                  
          return {apiData}         
        }catch(e){console.log(e)}  
       },
    created(){
        this.articles = this.convertTheArray(this.apiData);    
    },
    methods: {
      noumberOfCards: function(){
              return 7;
      },
      noumberOfSliders:function(articles){
        return Math.floor(articles.length/this.noumberOfCards() + 1);
      },
      convertTheArray:function (articles){
        var arrayRow = Array();
        var arrayCompleated = Array();        
        var indicator = 0;
        for(var i=0; i <=this.noumberOfSliders(articles) - 1 ; i++){
          for(var j=0; j<=this.noumberOfCards() - 1 ; j++){
            arrayRow.push({title: articles[indicator].title ,
                      snippet: articles[indicator].snippet, 
                      image: articles[indicator].image
            });
            indicator++;
            if(indicator >= articles.length){
                break;
            }
          }
           arrayCompleated.push(arrayRow);
           arrayRow = Array();
        }
        return arrayCompleated;
      }
    },
    data: ()=>({
      articles: Array(),
            swiperOption: {
              initialSlide:3,
              loop:true,              
              spaceBetween: -10,                       
                 navigation: {
                    nextEl: '.swiper-button-next',
                    prevEl: '.swiper-button-prev',
                 },
            }                    
    })
  };

  

</script>

<style>


 @media (max-width: 767.98px) {
   .medium-plus-screens{
     display: none;
   }
  
.swiper-container{
     overflow:hidden;
  }
  }
  @media (min-width: 767.98px) {
   .small-screens{
     display: none;
   }
  .swiper-container{
     overflow:visible;
  }
  ::-webkit-scrollbar {
    width: 0px;
    background: transparent; /* make scrollbar transparent */
}
  }

</style>
