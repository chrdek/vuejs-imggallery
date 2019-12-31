<template>
<div id="bg-parll__el" class="mainpllx--container">
  <div id="app">
    <FilteringListLayout title="Filter images"/>
    <ImagesListMain heading="List of Pictures Loaded"/>
  </div>
</div>
</template>

<script>
import ImagesListMain from './components/ImagesListMain.vue'
import FilteringListLayout from './components/FilteringListLayout.vue'
export default {
  name: 'app',
  components: {
  ImagesListMain,
  FilteringListLayout
  }
}
</script>

<style>
body,h2 { margin:0 }

#bg-parll__el{
  background-image: url("https://images.wallpaperscraft.com/image/camera_background_lens_77036_1280x720.jpg");
  background-size: 100%;
  background-repeat: no-repeat;
  background-size: cover;
  background-position:center;
  background-attachment: fixed;
}

.mainpllx--container{
  height: 100vh;
  width: 100vw;
  padding-top: 20vh;
  background-attachment: fixed;
  background-size: cover;
  background-repeat: no-repeat;
}

@media (min-width: 768px) {
	bg-parll__el{
	background-image:url("https://images.wallpaperscraft.com/image/camera_background_lens_77036_1280x720.jpg");
 }
}

#mainpllx__backel{
  background-attachment:fixed;
  background-size:cover;
  background-repeat: no-repeat;
  background-image: url("http://caraujo_pens.surge.sh/images/uZlR2bB.jpg");
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
