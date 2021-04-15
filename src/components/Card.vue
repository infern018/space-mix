<template>
  <div class="card" @click="selectCard" :class="flippedStyles">
      <div  class="card-face is-front">
          <img :src="`/images/${value}.png`" :alt="value" class="card-img">
          <img v-if="matched" src="../../public/images/checkmark.png" class="checkmark">
      </div>
      <div  class="card-face is-back" style="color:black; font-size:2rem">
      </div>
  </div>
</template>

<script>
import { computed } from 'vue'
export default {
    props:{
        matched:{
            type:Boolean,
            default:false
        },
        position:{
            type:Number,
            required:true
        },
        value:{
            type:String,
            required:true
        },
        visible:{
            type:Boolean,
            default:false
        }
    },
    setup(props, context){

        const flippedStyles = computed(() => {
            if(props.visible){
                return 'is-flipped'
            } else {
                return null
            }
        })

        const selectCard = () => {
            context.emit('select-card', {
                position: props.position,
                faceValue: props.value
            })
        }

        return{
            selectCard,
            flippedStyles
        }
    }
}
</script>

<style>

.card{
  position: relative;
  transition: 0.5s transform ease-in;
  transform-style: preserve-3d;
}

.card.is-flipped{
    transform: rotateY(180deg);
}

.card-face{
    width: 100%;
    height:100%;
    position: absolute;
    border-radius: 10px;
    backface-visibility: hidden;
}

.card-face.is-front{
    background-color: rgb(226, 227, 245);
    /* background-image: url('../../public/images/bgcard.jpg'); */
    color:white;
    transform: rotateY(180deg);

}

.card-face.is-back{
    background-color: #ff9d00;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' viewBox='0 0 1600 800'%3E%3Cg stroke='%23000' stroke-width='66.7' stroke-opacity='0.05' %3E%3Ccircle fill='%23ff9d00' cx='0' cy='0' r='1800'/%3E%3Ccircle fill='%23fb8d17' cx='0' cy='0' r='1700'/%3E%3Ccircle fill='%23f47d24' cx='0' cy='0' r='1600'/%3E%3Ccircle fill='%23ed6e2d' cx='0' cy='0' r='1500'/%3E%3Ccircle fill='%23e35f34' cx='0' cy='0' r='1400'/%3E%3Ccircle fill='%23d85239' cx='0' cy='0' r='1300'/%3E%3Ccircle fill='%23cc453e' cx='0' cy='0' r='1200'/%3E%3Ccircle fill='%23be3941' cx='0' cy='0' r='1100'/%3E%3Ccircle fill='%23b02f43' cx='0' cy='0' r='1000'/%3E%3Ccircle fill='%23a02644' cx='0' cy='0' r='900'/%3E%3Ccircle fill='%23901e44' cx='0' cy='0' r='800'/%3E%3Ccircle fill='%23801843' cx='0' cy='0' r='700'/%3E%3Ccircle fill='%236f1341' cx='0' cy='0' r='600'/%3E%3Ccircle fill='%235e0f3d' cx='0' cy='0' r='500'/%3E%3Ccircle fill='%234e0c38' cx='0' cy='0' r='400'/%3E%3Ccircle fill='%233e0933' cx='0' cy='0' r='300'/%3E%3Ccircle fill='%232e062c' cx='0' cy='0' r='200'/%3E%3Ccircle fill='%23210024' cx='0' cy='0' r='100'/%3E%3C/g%3E%3C/svg%3E");
    background-attachment: fixed;
    background-size: cover;
    color:white;
}

.card-img{
    position: relative;
    width: 90px;
    height: 90px;
}

.checkmark{
    position: absolute;
    width: 20px;
    height: 20px;
    right:3px;
    bottom:3px;
}

@media screen and (max-width: 480px) {
    .card-img{
        width: 60px;
        height: 60px;
    }
}

</style>