<template>
  <div id="app" style="background:url(./components/1.jpg) no-repeat">
   <mt-header fixed title="彬狗音乐播放器" class="header"></mt-header>
   <mt-search v-model="value" cancel-text="取消" placeholder="搜索">
     <mt-cell-swipe 
        v-for="item in result"
        :title="item.title"
        :right="[
    {
      content: '播放',
      style: { background: '#F5C6D9', color: '#fff' },
      handler: () => playMusic(item.id)
    }
    ]">
       
      </mt-cell-swipe>
    
</mt-search>
   <audio id = 'audio' :src="music_url"  autoplay="autoplay" >
    </audio>
  </div>
 
</template>

<script>
import Hello from './components/Hello'
import MessageLength from './components/MessageLength'
import aaaa from './music_api'
export default {
  name: 'app',
   data () {
    return {
      result:[],
      value:"",
      music_url: ""
    }
  },
  watch: {
    value: function (val, oldVal) {
      let that = this
      console.log('new: %s, old: %s', val, oldVal)
      aaaa.api.search(this,val,8, (response) => {
        console.log(response.body.result.songs)
        let songsArray=response.body.result.songs;
        let i;
        let result =[]
        for(i=0;i<songsArray.length;i++){
          result.push({title:songsArray[i].name+" "+" "+songsArray[i].artists[0].name,id:songsArray[i].id});
        }
        that.result = result
        console.log(that.result)
      })
    }
  },
  methods: {
    playMusic: function (event) {
     console.log(event);
      aaaa.api.detail(this,event, (response) => {
         this.music_url = response.body.songs[0].mp3Url
      })
      
    }
  },
  components: {
    Hello,
    MessageLength
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.header h1{
  font-weight:bold;

}
.header{
  background-color:lightpink !important;

}
.mint-search-list{
  padding-top:124px !important;
}

</style>
