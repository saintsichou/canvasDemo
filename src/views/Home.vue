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
      //绘制前先清除画布
      ctx.clearRect(0, 0, canvas.width, canvas.height)
      ctx.font = "48px serif";
      ctx.textAlign = "center";
      let txt1 = Math.floor(Math.random()*10+10);
      let txt2 = Math.floor(Math.random()*10+1);
      let x = ['*','+','-'];
      let calculate = x[Math.floor(Math.random()*3)]
      let fontText = `${txt1}${calculate}${txt2}=?`
      this.calc = {
        txt1,
        txt2,
        calculate
      }
      ctx.fillText(fontText, canvas.width/2, canvas.height/2);
      console.log(`${txt1}${x[Math.floor(Math.random()*3)]}${txt2}`)
      console.log(this.calc)

    },
    color16(){//十六进制颜色随机
			var r = Math.floor(Math.random()*256);
			var g = Math.floor(Math.random()*256);
			var b = Math.floor(Math.random()*256);
			var color = '#'+r.toString(16)+g.toString(16)+b.toString(16);
			return color;
    },
    verify(){
      if(this.calc){
        let result = 0
        switch(this.calc.calculate){
            case '+':
              result = this.calc.txt1 + this.calc.txt2
            break;
            case '-':
              result = this.calc.txt1 - this.calc.txt2
            break;
            case '*':
              result = this.calc.txt1 * this.calc.txt2
            break;
            default:
              result = this.calc.txt1 / this.calc.txt2
        }
        this.input == result ? alert('对') : alert('错误')
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