<template>
  <div id="app">
    <b-navbar
      type="dark"
      :variant="variant"
      ref="main-nav"
      id="main-nav"
      class="pl-3 pt-1 pb-1 m-0"
    >
      <b-navbar-brand href="#" to="/">
        <b-iconstack font-scale="1">
          <b-icon stacked icon="globe" animation="throb" variant="primary" scale="0.75" ></b-icon>
          <b-icon stacked icon="globe" animation="spin-reverse" :variant="variantLogo" ></b-icon>
        </b-iconstack> &nbsp;
        <span>UNIQ-VIS</span>
      </b-navbar-brand>
      <b-navbar-nav>
        <b-nav-item to="/SimulationList" >
          <span v-if="currentRoute.startsWith('Simulation')" style="color:skyblue"> <strong>트래픽시뮬레이션 </strong> </span>
          <span v-else> 트래픽시뮬레이션  </span>
        </b-nav-item>
        <b-nav-item to="/OptimizationList" >
          <span v-if="currentRoute.startsWith('Optimization')" style="color:skyblue"> <strong>신호최적화 </strong> </span>
          <span v-else> 신호최적화  </span>
        </b-nav-item>
      </b-navbar-nav>
        <b-navbar-nav class="ml-auto">
      <!-- <b-collapse is-nav id="nav_dropdown_collapse" > -->
          <b-nav-item size="sm" to="/SignalEditor" >
            신호편집
          </b-nav-item>
      <!-- </b-collapse> -->
        </b-navbar-nav>
    </b-navbar>
    <transition name="fade">
      <router-view/>
    </transition>

    <!--
      BOTTOM COPYRIGHT
    -->
    <!-- <b-card
      bg-variant="dark"
      text-variant="white"
      class="no-round-corner"
      v-if="currentRoute !== 'SimulationResultMap'"
    >
      <b-container fluid class="mt-2 mb-2 p-2 text-center" >
        도시 교통 문제 개선을 위한 클라우드 기반 트래픽 예측 시뮬레이션 소프트웨어
        <hr class="my-3">
        <small class="text-muted">Copyright 2020. ETRI All rights reserved.</small>
        <small class="text-muted">Copyright ⓒ 2020. <em>Modutech</em> Inc. All rights reserved.</small>
      </b-container>
    </b-card> -->
  </div>
</template>

<script>
import userState from '@/user-state';

export default {
  name: 'App',
  mounted() {
    this.prevScrollpos = window.pageYOffset;
    // const navBar = this.$refs['main-nav'];
    // window.onscroll = () => {
    //   const currentScrollPos = window.pageYOffset;
    //   if (this.prevScrollpos > currentScrollPos) {
    //     navBar.$el.style.top = '0';
    //   } else {
    //     navBar.$el.style.top = '-50px';
    //   }
    //   this.prevScrollpos = currentScrollPos;
    // };
    // const variants = ['success','danger', 'warning', 'primary', 'light']
    const variants = ['light', 'secondary']
    let i = 0;
    setInterval(() => {
      this.variantLogo = variants[i++ % variants.length]
      if ( i >= 100) {
        i = 0
      }
    }, 1000)

    // $router.currentRoute.name
  },

  watch:{
    $route (to, from){
      this.currentRoute = to.name
    }
  },
  data() {
    return {
      prevScrollpos: window.pageYOffset,
      variant: 'dark',
      userState,
      variantLogo: 'dark',
      currentRoute: '',
    };
  },

};
</script>

<style scoped>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 0px;
}

.fade-enter-active, .fade-leave-active {
  transition-property: opacity;
  transition-duration: .25s;
}

.fade-enter-active {
  transition-delay: .25s;
}

.fade-enter, .fade-leave-active {
  opacity: 0;
}

.btn .fa-icon {
  vertical-align: middle;
  margin-right: 0.5rem;
}
.btn .fa-icon:last-child {
  margin-right: 0;
}

#main-nav {
  transition: top 0.3s;
}

html {
  background: lightgrey;
  overflow: hidden;
}

* {
  box-sizing: border-box;
}
.no-round-corner {
  border-radius: 0
}
</style>
