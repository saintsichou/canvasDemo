<!--
 * @Date: 2020-03-03 19:50:36
 * @LastEditors  : Lee
 * @LastEditTime : 2020-03-05 21:11:38
 -->
<template>
  <div>
    <canvas id="draw" width="550" height="350" @click="draw"></canvas>
    <button @click='clear'>清除画布</button>
    <button @click='exportPng'>导出画布</button>
  </div>
</template>

<script>
  export default {
    data(){
      return {

      }
    },
    mounted(){
      this.draw()
    },
    methods:{
      draw(){
        let canvas = document.getElementById('draw')
        let ctx = canvas.getContext('2d')
         canvas.addEventListener('touchstart',function(e){
            e.preventDefault();
            let _x = e.touches[0].pageX
            let _y = e.touches[0].pageY
            ctx.beginPath();
            //寻找落笔点
            ctx.moveTo(_x - canvas.offsetLeft,_y - canvas.offsetTop);
            this.addEventListener('touchmove',function(e){
              let x = e.touches[0].pageX
              let y = e.touches[0].pageY
            //绘制线条
              ctx.lineTo(x-canvas.offsetLeft,y-canvas.offsetTop),
              ctx.stroke();
            }),
            this.addEventListener('touchend',function(){
              ctx.closePath();
            })
         })
      },
      //清除画布
      clear(){
        let canvas = document.getElementById('draw')
        let ctx = canvas.getContext('2d')
        ctx.clearRect(0,0,canvas.width,canvas.height)
      },
      //导出图片
      exportPng(){
        let canvas = document.getElementById('draw')
        let ctx = canvas.getContext('2d')
        let oimg = new Image()
        ctx.drawImage(oimg,0,0)
        oimg.src = canvas.toDataURL('image/png');
        document.body.appendChild(oimg)
      }
    }
  }
</script>

<style scoped>
#draw{
  border:1px solid #000;
  background: #3333;
}
</style>