<template>
  <div>
    <button @click="showCrop('144,2152,120,1252')">Show Crop</button>
    <button @click="isShow=false">Reset</button>
    <canvas style="display:none" id="canvas" width="25px" height="25px"></canvas>
    <img v-if="!isShow" id="imageCanvas" :src="urlImage" alt="">
    <img v-else :src="cropImage" alt="">
  </div> 
</template>

<script>
export default {
  data() {
    return {
      urlImage: 'public/img/img_test.JPG',
      cropImage: '',
      isShow: false,
      coordinates: []
    }
  },
  //Las coordenadas deben seran obtenidas por ajax
  // coordinates test 144,2152,120,1252
  methods: {
    showCrop: function (wxyz) {
      let str = wxyz
      let wxyzArr = str.split(',')
      // console.log(wxyzArr)
      this.loadCanvas(wxyzArr)
    },
    loadCanvas: function (coord) {
      let newImage = document.getElementById('imageCanvas')
      let canvas = document.getElementById('canvas')
      let context = canvas.getContext('2d')
      let w = coord[0]
      let x = coord[2]
      let y = coord[1]
      let z = coord[3] - x
      var destWidth = newImage.naturalWidth
      var destHeight = newImage.naturalHeight
      canvas.width = destWidth
      canvas.height = destHeight
      context.fillStyle = "rgba(255, 0, 0, 0.3)"
      context.drawImage(newImage,0,0)
      context.fillRect(w,x,y,z)
      let img = canvas.toDataURL("image/png")
      this.cropImage = img
      this.isShow = true
    }
  }
}
</script>

<style>
img{
  width: 100%;
}
</style>
