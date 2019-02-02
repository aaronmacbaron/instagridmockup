<template>
  <div id="wrapper">
    <main>
        <div class="container">
          <h3 class="title">Grid Planner</h3>
          <p style="text-align:center;">
            After you have selected some images for your grid, left clicking an image tells the app that you want to switch the positioning of that image to another one that is in the grid. You can see what image is currently selected for switching in the bottom left of the application window. Clicking a second image will switch the positions of the initially selected image and the one you just clicked.  
          </p>
          <br />
          <p style="text-align:center;">To remove an image from the grid, simply double click it.</p>
          <br />
          <a href="javascript:void(0);" @click="rowCount <= rowLimit ? rowCount++ : nothing" class="row-incrementor">+</a>
          <a href="javascript:void(0);" @click="rowCount > 1 ? rowCount-- : nothing" class="row-decrementor">-</a>
          <div class="grid-row" :key="'grid-row-'+i" v-for="i in rowCount">
            <grid-item 
              class="grid-item" 
              :key="'grid-item-'+i+'-'+k" 
              :id="'grid-item-'+i+'-'+k"
              v-for="k in 3"/>
          </div>
          <div v-if="switchingObject" class="switching-interface">
            <img :src="switchingObject.filename"/>
          </div>
        </div>
    </main>
  </div>
</template>

<script>
  import SystemInformation from './LandingPage/SystemInformation'
  import GridItem from './GridItem/GridItem'

  export default {
    name: 'landing-page',
    components: { SystemInformation, GridItem },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
      },
      nothing(){}
    },
    data : function(){
      return {
        rowCount : 1,
        rowLimit : 10,
        switchingObject : null
      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  h3.title{
        text-align: center;
      margin: 20px auto;
      font-size: 36px;
  }
  .switching-interface{
    position:fixed;
    width:100px;
    height:100px;
    box-shadow:1px 1px 8px #333;
    bottom:20px;
    left:20px;
  }
  .switching-interface img{
    width:100px;
    height:100px;
  }
  a.row-incrementor{
    text-decoration:none;
    color:white;
    background:teal;
    font-size:36px;
    line-height:20px;
    float:right;
    display:block;
    position:absolute;
    top:30px;
    right:20px;
    border:1px solid teal;
    transition: all .4s linear;
    padding:5px;
  }
  a.row-incrementor:hover{
    background:white;
    color:teal;
  }
  a.row-decrementor{
    text-decoration:none;
    color:white;
    background:crimson;
    font-size:36px;
    line-height:20px;
    float:right;
    display:block;
    position:absolute;
    top:30px;
    right:60px;
    border:1px solid crimson;
    padding:5px 8px;
    transition: all .4s linear;
  }
  a.row-decrementor:hover{
    background:white;
    color:crimson;
  }
  div.grid-row{
    position:relative;
    margin:0 auto;
    margin-bottom:3px;
    display:flex;
    flex-direction: horizontal;
  }
  div.grid-item{
    display:flex;
    flex:1 0 0%;
    align-items:stretch;
    margin-right:0.095%;
    display:inline-block;
    background:#ccc;
    overflow:hidden;
  }
  div.grid-item:last-of-type{
    margin-right:unset;
  }
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body { font-family: 'Source Sans Pro', sans-serif; background:#fff;}

  #wrapper {
    background:
      radial-gradient(
        ellipse at top left,
        rgba(255, 255, 255, 1) 40%,
        rgba(229, 229, 229, .9) 100%
      );
    height: 100vh;
    padding: 10px 10px;
    width: 100vw;
  }

  #logo {
    height: auto;
    margin-bottom: 20px;
    width: 420px;
  }

  main {
    display: block;
    justify-content: space-between;
  }
</style>
