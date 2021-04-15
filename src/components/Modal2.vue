<template>
      <!-- Modal HTML -->
        <!-- The Modal -->
        <div id="myModal2" class="modal2" ref="myModal2">

        <!-- Modal content -->
        <div class="modal2-content">
            <span class="close" @click="handleClickBtn">&times;</span>
            <p>A card matching game made in Vue-3, each card has its similar pair that can be revealed by clicking on it, go ahead, click "START" and see in how many least clicks you can reveal them all! :)</p>
        </div>

    </div>

</template>

<script>

export default {
    name:'Modal2',
    methods:{
        handleClickBtn(){
            this.$refs.myModal2.style.display = "none"
        }
    }
}
</script>

<style>


.modal2 {
  display: show; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 190px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal2-content {
  text-align: left;
  background-color: rgba(13, 20, 44, 0.9);
  border-radius: 10px;
  margin: auto;
  padding: 20px;
  width: 25%;
  font-size: 18px;
  line-height: 25px;
  word-spacing: 0.4em;
  font-family: 'Zen Dots', cursive;
}

/* The Close Button */
.close {
  color: #fff;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: rgb(131, 131, 131);
  text-decoration: none;
  cursor: pointer;
}

@media screen and (max-width: 480px) {
    .modal2-content{
        padding:10px;
        font-size: 12px;
        width: 60%;
        line-height: 20px;
        word-spacing: 0.2em;
    }
}


</style>