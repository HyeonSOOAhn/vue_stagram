<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step==1" @click="step++">Next</li>
      <li v-if="step==2" @click="publish">발행</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>
  <h4>{{$store.state.name}}</h4>
  <button @click="$store.commit('이름변경')">버튼</button>
  <h4>{{$store.state.age}}</h4>
  <button @click="$store.commit('나이올리기',10)">버튼</button>

  <p>{{$store.state.more}}</p>
  <button @click="$store.dispatch('getData')">더보기버튼</button>

  <Container @write="write = $event" :datas="datas" :step="step" :url="url" :filter="filter"/>
  <button @click="more">더보기</button>

  <p>{{now2}} {{카운터}}</p>
  <button @click="카운터++">버튼</button>

  <p>{{name}}</p>

  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>


</template>

<script>
import Container from './components/Container.vue';
import datas from './data.js';
import axios from 'axios';

export default {
  name: "App",
  data() {
    return {
      카운터 : 0,
      filter : '',
      url : '',
      step : 0,
      datas : datas,
      moreCount : 0,
      write : '',
    }
  },
  mounted() {
    this.emitter.on('filter',(a)=>{
      this.filter=a;
    })
  },
  components: {
    Container,
  },

  computed : {
    now2() {
      return new Date();
    },
    name() {
      return this.$stroe.state.name;
    }
  },

  methods : {
    now() {
      return new Date();
    },

    publish(){
      var 내게시물 = {
        name: "Kim Hyun",
        userImage: "https://placeimg.com/100/100/arch",
        postImage: this.url,
        likes: 36,
        date: "May 15",
        liked: false,
        content: this.write,
        filter: "perpetua"
        };
      this.datas.unshift(내게시물);
      this.step = 0;
    },
    more() {
        axios.get(`https://codingapple1.github.io/vue/more${this.moreCount}.json`)
        .then((result) =>{
          this.datas.push(result.data);
        });
        this.moreCount++;
    },
    upload(e) {
      let a = e.target.files;
      this.url = URL.createObjectURL(a[0]);
      this.step++;
    },


  }
};
</script>

<style>
@import './style.css';
</style>
