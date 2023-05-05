<template>
    <div class="">
        <HeaderApp />
        <SlideApp />
        <div class="jumbotron p-3 p-md-5 text-white rounded bg-dark">
            <body>
  <section class="about-us">
    <div class="about">
      <div class="text">
        <h2>About Us</h2>
        <h5>Front-end Developer & <span>Designer</span></h5>
          <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Expedita natus ad sed harum itaque ullam enim quas, veniam accusantium, quia animi id eos adipisci iusto molestias asperiores explicabo cum vero atque amet corporis! Soluta illum facere consequuntur magni. Ullam dolorem repudiandae cumque voluptate consequatur consectetur, eos provident necessitatibus reiciendis corrupti!</p>
        <div class="data">
        <a href="#" class="hire">Hire Me</a>
        </div>
      </div>
    </div>
  </section>
</body>
          </div>
        <FooterApp />
    </div>
</template>

<script>
import HeaderApp from '../../components/main/HeaderApp.vue'
import FooterApp from '../../components/main/FooterApp.vue'
import SlideApp from '../../components/main/SlideApp.vue'
export default{
    name: "ContactPage",
    components: {
        HeaderApp,
        FooterApp,
        SlideApp
    }
}
</script>

<style scoped>

.mapouter{position:relative;text-align:right;width:100%;height:400px;}.gmap_canvas {overflow:hidden;background:none!important;width:100%;height:400px;}.gmap_iframe {width:100%!important;height:400px!important;}


.about-us{
  width: 100%;
}

.about{
  max-width: 85%;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

span{
  color: #4070f4;
}
.text p{
  font-size: 18px;
  line-height: 25px;
  letter-spacing: 1px;
}

.hire{
  font-size: 18px;
  background: #4070f4;
  color: #fff;
  text-decoration: none;
  border: none;
  border-radius: 6px;
  transition: 0.5s;
}
.hire:hover{
  background: #000;
  border: 1px solid #4070f4;
}
</style>