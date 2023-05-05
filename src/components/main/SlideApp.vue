<template>
    <div class="container-fluid" >
        <div id="demo" class="jumbotron jumbotron-fluid" >
            <div class="container">
              <h1 class="text-center">Computer Science Blog</h1>
              <p class="text-center">Academic and Computer Scientist.</p>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    name: "SlideApp"
}
</script>

<style scoped>
#demo{
    opacity: 0.8;
    background: linear-gradient(90deg, rgba(255, 255, 255, 0.1) 0%, rgba(255, 255, 255, 0.1) 100%), url(https://cdn.pixabay.com/photo/2018/02/23/04/38/computer-3174729_960_720.jpg);
    background-position: center;
}
</style>