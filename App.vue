<template>
<div id="app">
  <header>
    <h1>My Music</h1>
  </header>
  <main>
    <section class="player">
      <h2 class="song-title">{{current.title}} - <span>{{current.artist}}</span></h2>
<div class="controls">
  <button class="prev" @click="prev">Prev</button>
  <button class="play" v-if="!isPlaying" @click="play">Play</button>
  <button class="pause" v-else @click="pause">Pause</button>
  <button class="next" @click="next">Next</button>
</div>

  <section class="playlist">
    <h3>The Play List</h3>
    <button v-for="song in songs"

    :key="song.src"
    @click="play(song)" :class="(song.src === current.src) ?  'song playing' : 'song'"
    >{{song.title}} - {{song.artist}} {{isPlaying ? ' -- now playing ' : ""}}
  </button>
  </section>
    </section>
  </main>

</div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [{
          title: 'vacaciones',
          artist: 'Dj David crowd',
          src: require('./assets/Vacaciones.mp3')
        },
        {
          title: 'mix2',
          artist: 'Dj David crowd',
          src: require('./assets/bonita.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play(song) {
      if(typeof song.src != "undefined"){
        this.current=song;

        this.player.src =this.current.src;
      }
      this.player.play();
      this.isPlaying=true;
    },
    pause(){
      this.player.pause();
      this.isPlaying=false;
    },
    next(){
      this.index++;
      if (this.index >this.songs.length-1){
        this.index=this.songs.length-1;
      }
      this.current=this.songs[this.index];
      this.play(this.current);
    },
    prev(){
    this.index--;
    if(this.index<0){
      this.index = this.songs.length - 1;
    }
    this.current = this.songs[this.index];
    this.play(this.current);
    }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
     //this.player.play();

  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #EEE;

}


main{
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;


}
.song-title{
  color:#53565A;
  font-size: 30px;
  font-weight: 700px;
  text-transform: uppercase;
  text-align: center;
  margin-bottom: 20px;
}
.song-title span{
  font-weight: 400;
  font-style: italic;
}


.controls{
  display: flex;
  justify-content: center;
  align-items: center;
  padding:30ox 15px;
  margin-bottom: 50px;

}

button{
  appearance:none;
  background:none;
  border:none;
  outline: none;
  cursor:pointer;
}

.play{
  font-size: 20px;
font-weight: 700;
padding: 15px 25px;
margin: 0px 15px;
border-radius: 8px;
color:#fff;
background-color: rgb(29, 161, 101);
}

.pause{
  font-size: 20px;
font-weight: 700;
padding: 15px 25px;
margin: 0px 15px;
border-radius: 8px;
color:#fff;
background-color: #CC2E5D;
}

.next, .prev {
  font-size: 16px;
font-weight: 700;
padding: 10px 20px;
margin: 0px 15px;
border-radius: 6px;
color:#fff;
background-color: #FF5E5E;
}
.playlist{
  padding: 0px 20px;

}

.playlist h3{
  color:#212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 15px;
  text-align: center;


}


.playlist .song{
  display:block;
  width: 100%;
  padding: 15px;
  font-size:20px;
  font-weight: 700;
  cursor:pointer;
}

.playlist .song:hover{
  color:#ff5858;
}
.playlist .song.playing{
  color:#fff;
  background-image: linear-gradient(to right, #CC2E5D,#FF5858 );
}
</style>
