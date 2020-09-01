<template>   
        <div  class="card">
           <img class="card__img card-img" :src="image"  alt="Card image">
           <div class="card__info card-img-overlay p-1 text-center">
               <div class="card__title card-title ">{{title}}</div>
               <div class="card__desc card-text ">{{description}}</div>        
            </div>
        </div>    
</template>

<script>

    export default {
        name:'card',
        props: {
            title:{
                type:String,
                default:""
            },
            description:{
                type:String,
                default:""
            }, 
            image:{
                type:String,
                required:true
            }   
        }, 
    };
</script>

<style lang="scss">

    $color-white :#fff;
    $color-black : #000;
    $color-80black : #222;

    @mixin maxsize(){
        width: 100%;
        height: 100%;
    }

    @mixin posabstopleft(){
        position: absolute;
        top: 0;
        left: 0;
    }

    *{        
        font-family: 'Lato' , sans-serif;
    }

    html,body{
      //  @include maxsize();
        background: $color-80black;
    }  
    .card{
        height: 100px;
        background: $color-white;
        position: relative;
        display: flex;
        align-items: flex-end;
        box-shadow: 0px 7px 10px rgba(0,0,0,0.5);
        transition: 0.5s ease-in-out;
        .card__img{
            @include maxsize();
            @include posabstopleft();
            object-fit:  cover;           
        }
    }
    .card{
        .card__info{
            position: relative;
            z-index: 3;
            color: $color-white;
            transition: 0.5s all;
            .card__title{
               margin: 0;
               font-size: 0.8rem;
                
            }
        }
    }

   .card {
        .card__info{
            .card__desc{
                letter-spacing: 1px;
                font-size: 0.5rem;
                margin-top: 8px;
                margin-bottom: 20px;
            }
        }
    }

    .card {
        .card__info{
            .card__link{
                text-decoration: none;
                padding: 0.5rem 1rem;
                background:  $color-white;
                color: $color-black;
                font-size: 14px;
                font-weight: bold;
                cursor: pointer;
                transition: 0.4s ease-in-out;
            }
        }
    }

    .medium-plus-screens {
            .card:hover{
                -webkit-transform: scale(1.5); 
                -ms-transform: scale(1.5);
                z-index: 4 !important; 
            }
    }

    .card:before{
        content: "";
        @include posabstopleft();
        @include maxsize(); 
        display: block;        
        background: linear-gradient(to bottom ,rgba(0,176,155,0.5) , rgba(150,201,61,1));
        z-index: 2;
        transition: 0.5s all;
        opacity: 0;
    }

    .card:hover:before{
        opacity: 1;
    }

   
    .card:hover {
        .card__info{
            display: block;
            opacity: 1;          
            overflow: hidden;
            text-overflow: ellipsis;
        }
    }

 
    .card{
        .card__info{
            display: none;
            .card__link:hover{
                box-shadow: 0px 7px 10px rgba(0,0,0,0.5);
            }
        }
    }

</style>