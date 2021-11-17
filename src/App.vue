<template>
  <div id="app">
    <div class="timerBox">
      <img src="./assets/cronometro.png" alt="img" class="img">
      <a class="timer">{{numero}}</a>
    </div>

    <div class="areaBtn">
      <button class="botao" @click="vai">{{ botao }}</button>
      <button class="botao" @click="limpar">LIMPAR</button>
    </div>

    <div class="list" v-show="historico.length > 0">
      <ul>
        <li v-for="(item, index) in historico" :key="index">
          VOCE FEZ UMA PAUSA EM: {{item}}
        </li>
      </ul>
      <button @click="historico = []">Limpar histórico</button>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      numero: 0,
      botao: 'VAI',
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
      historico: []
    }
  },
  methods: {
    vai(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
        this.botao = 'VAI';
        if(this.ss !== 0){
          this.historico.push(this.numero);
        }
      }else{
        this.timer = setInterval(()=> {
          this.rodarTimer()
        }, 100);
        this.botao = 'PAUSAR';
      }
    },
    limpar(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
      }
      this.ss = 0;
      this.mm = 0;
      this.hh = 0;
      this.numero = 0;
      this.botao = 'VAI';
      this.historico = [];
    },
    rodarTimer(){
      this.ss++;

      if(this.ss == 59){
        this.mm++;
        this.ss = 0;
      }

      if(this.mm == 59){
        this.hh++;
        this.mm = 0;
      }

      let format = (this.hh < 10 ? '0'+this.hh : this.hh) + ':'
      + (this.mm < 10 ? '0'+this.mm : this.mm) + ','
      + (this.ss < 10 ? '0'+this.ss : this.ss);

      return this.numero = format;

    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  #app {
    display: flex;
    width: 100%;
    min-height: 100vh;
    align-items: center;
    justify-content: flex-start;
    flex-direction: column;
    padding-top: 30px;
  }

  .timerBox{
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .img {
    width: 55vh;
  }

  .timer {
    color: #FFF;
    font-size: 70px;
    position: absolute;
    margin-top: 40px;
  }

  .areaBtn {
    margin-top: 20px;
    display: flex;
  }

  .botao {
    width: 150px;
    background-color: #FFF;
    font-size: 20px;
    border: none;
    border-radius: 5px;
    text-align: center;
    margin: 10px 15px;
    padding: 6px;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    transition: .5s all;
  }

  .botao:hover {
    opacity: 0.7;
  }

  ul {
    text-align: center;
    padding: 0;
  }

  ul li {
    margin-top: 4px;
    padding: 15px;
    background-color: rgb(70,70,70);
    list-style: none;
    color: #FFF;
    font-size: 18px;
    border-radius: 6px;
  }

  .list {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
  }

  .list button {
    cursor: pointer;
    border: none;
    background-color: #FFF;
    padding: 8px;
    border-radius: 5px;
    margin: 12px 0;
  }
</style>
