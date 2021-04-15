<template>
      <!-- Modal HTML -->
        <!-- The Modal -->
        <div id="myModal" class="modal" ref="myModal">

        <!-- Modal content -->
        <div class="modal-content">
            <span class="close" @click="handleClickBtn">&times;</span>
            <p>CLICKS: {{ score }}</p>
        </div>

    </div>

</template>

<script>

export default {
    name:'Modal',
    props:['score'],
    methods:{
        handleClickBtn(){
            this.$refs.myModal.style.display = "none"
        }
    }
}
</script>

<style>


.modal {
  display: show; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  padding-top: 250px; /* Location of the box */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  background-color: rgba(13, 20, 44, 0.9);
  border-radius: 10px;
  margin: auto;
  padding: 20px;
  width: 25%;
  font-size: 25px;
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

</style>