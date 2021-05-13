<template>
	<div id="box">
    <!-- <Cat></Cat> -->
		<Muxiang></Muxiang>
    <!-- <Feichuan></Feichuan>
    <Female></Female>	 -->
	</div>
</template>

<script>
// import Cat from './components/Cat'
import Muxiang from './components/Muxiang'
// import Feichuan from './components/Feichuan'
// import Female from './components/Female'

export default {
  name: 'App',
  components: {
    // Cat,
		Muxiang,
    // Feichuan,
    // Female
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#box{
    color: #000;
    font-family: Monospace;
    font-size: 13px;
    text-align: center;
    font-weight: bold;
    margin: 0px;
    overflow: hidden;
    width:100%;
    height:100%;
}
</style>

