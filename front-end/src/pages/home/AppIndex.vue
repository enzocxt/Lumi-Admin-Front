<template>
  <div style="margin-top: 40px">
    <side-menu id="side-menu"></side-menu>
    <div class="home">
      <div id="header-div">
        <div style="height: 30px"></div>
        <quick-nav style="float: left;"></quick-nav>
        <carousel></carousel>
      </div>
      <update-card id="update-card"></update-card>
      <slogan id="slogan"></slogan>
      <about id="about"></about>
    </div>
  </div>
</template>

<script>
import Carousel from './Carousel'
import QuickNav from './QuickNav'
import UpdateCard from './UpdateCard'
import SideMenu from './SideMenu'
import Slogan from './Slogan'
import About from '@/components/common/About'
export default {
  name: 'AppIndex',
  components: {Carousel, QuickNav, Slogan, About, UpdateCard, SideMenu}
}
</script>

<style scoped>
.home {
  width: 990px;
  margin-left: auto;
  margin-right: auto;
  margin-top: -20px;
}
#header-div {
  padding-bottom: 20px;
  padding-left: 5px;
  background-color: white;
}
#side-menu {
  position: fixed;
  margin-left: 50%;
  left: -680px;
  top: 100px;
}
</style>