<template>
  <div class="home">

    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <canvas id="can" width="550" height="350" @click="draw">浏览器不支持canvas,请切换</canvas>
    <div><input type="text" v-model="input"></div> <button @click="verify">验证</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data() {
    return {
      input:'',
      calc:{}

    }
  },
  mounted () {
    this.draw()
  },
  methods: {
    //绘制图形
    draw() {
      let canvas = document.getElementById('can');
      let ctx = canvas.getContext('2d');
      ctx.clearRect(0, 0, canvas.width, canvas.height)
      let sCode = "a,b,c,d,e,f,g,h,i,j,k,m,n,p,q,r,s,t,u,v,w,x,y,z,A,B,C,E,F,G,H,J,K,L,M,N,P,Q,R,S,T,W,X,Y,Z,1,2,3,4,5,6,7,8,9,0";
      let aCode = sCode.split(",");
      ctx.font = "48px serif";
      ctx.textAlign = "center";
      let datas=[]
      for (let i = 0; i < 4; i++) {
          let results = aCode[Math.floor(Math.random()*aCode.length)]//取随机数
          // var x = canvas.width/2-50 + i * 50;//文字在canvas上的x坐标
          // var y = canvas.height/2;//文字在canvas上的y坐标
          var deg = Math.floor(Math.random() * 15);
          // ctx.translate(x, y);
          console.log(deg)
          ctx.rotate(deg*Math.PI/180);
          datas.push(results)
          ctx.fillText(results ,canvas.width/2-60+i*60, canvas.height/2) //绘制
          ctx.rotate(-deg*Math.PI/180);
          // ctx.translate(-x, -y);
          ctx.fillStyle = this.color16();
      }
      for (let i = 0; i <= 5; i++) { //验证码上显示线条
          ctx.strokeStyle = this.color16();
          ctx.beginPath();
          ctx.moveTo(Math.random() * canvas.width, Math.random() * canvas.height);
          ctx.lineTo(Math.random() * canvas.width, Math.random() * canvas.height);
          ctx.stroke();
      }
      for (let i = 0; i <= 30; i++) { //验证码上显示小点
          ctx.strokeStyle = this.color16();
          ctx.beginPath();
          var x = Math.random() * canvas.width;
          var y = Math.random() * canvas.height;
          ctx.moveTo(x, y);
          ctx.lineTo(x + 1, y + 1);
          ctx.stroke();
        }
      this.calc = datas
    },
    color16(){//十六进制颜色随机
			var r = Math.floor(Math.random()*256);
			var g = Math.floor(Math.random()*256);
			var b = Math.floor(Math.random()*256);
			var color = '#'+r.toString(16)+g.toString(16)+b.toString(16);
			return color;
    },
    //验证
    verify(){
      if(this.calc){
        let str = this.calc.join('').toUpperCase()
        console.log(str)
        this.input.toUpperCase() == str ? alert('对') : alert('错误') && this.draw()
      }else{
        alert('请输入验证码')
      }
    }
  },
}
</script>
<style scoped>
  #can{
    border:1px solid #000;
    cursor: pointer;
  }
</style>