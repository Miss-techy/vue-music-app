<template>
<div class="app">
  <header>
    <h1>My music</h1>
  </header>

    <main>
      <section class="player">

        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>

          </div>

      </section>

<section class="playlist">
  <h3>The Playlist</h3>
<button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 
'song playing' : 'song'"> {{song.title }} - {{song.artist}} </button>
</section>

    </main>


  

</div>
  
</template>

<script>

export default {
  name: 'App',
  data() {
    return{
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Clarity',
          artist: 'Andy Mineo',
          src: require('./assets/Andy Mineo_ Clarity.mp3')
        },
        {
          title: 'Light Work',
          artist: '116',
          src: require('./assets/Lecrae_Light Work.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {


    play(song) {   //play the song

      if( typeof song.src == 'undefined' ) {
        this.current == song;

        this.player.src = this.current.src
      }
      this.player.play();
      this.player.addEventListener('ended', function() {
        this.index++
        
        if(this.index > this.songs.length -1) {
  this.index = 0;

  this.current = this.songs[this.index];
  this.play(this.current)
}

      }.bind(this))
      this.isPlaying = true
    },



    pause() {         //pause the song

  this.player.pause();
  this.isPlaying = false
},



next() {      //play the next song

this.index++;
if(this.index > this.songs.length -1) {
  this.index = 0;

  this.current = this.songs[this.index];
  this.play(this.current)
}
},



prev() {  //play the previous song


  this.index--;
if(this.index < 0) {
  this.index = this.songs.length -1;

  this.current = this.songs[this.index];
  this.play(this.current)

}
}

  },

  

created() {
  this.current = this.songs[this.index];
  this.player.src =this.current.src;

}
  
}
</script>

<style>

*{
  margin:0;
  padding:0;
  box-sizing: border-box;
}

body{
  font-family: sans-serif;
}
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background: #212121;
  color: #fff;
}

main{
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.song-title{
  color: #53565a;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span{
  font-weight: 400;
  font-style: italic;
}

.controls{
  display:flex;
  justify-content: center;
  padding:30px 15px;
}

button{
  appearance: none;
  outline:none;
  border: none;
  background:none;
  cursor: pointer;
}

.play{
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0 15px;
  border-radius: 8px;
  color: #fff;
  background: #cc2e5d;
}

button:hover{
  opacity:0.7
}
</style>
