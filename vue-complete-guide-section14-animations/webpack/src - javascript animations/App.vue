<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Animations</h1>
                <hr>
                <select v-model="alertAnimation" class="form-control">
                  <option value="fade">Fade</option>
                  <option value="slide">Slide</option>
                </select>

                <transition :name="alertAnimation">
                  <div class="alert alert-info" v-show="show">This is some alert</div>
                </transition>

                <br>
                <button class="btn btn-primary" @click="show = !show">Show Alert</button>

                <hr>
                <br><br>
                <transition :name="alertAnimation" mode="out-in">
                  <div class="alert alert-info" v-if="show" key="info">This is some alert</div>
                  <div class="alert alert-warning" v-else key="warning">This is some warning</div>
                </transition>

                <hr>
                <h2>JAVASCRIPT ANIMATIONS</h2>
                <button class="btn btn-primary" @click="load = !load">Load / Remote Element</button>
                <br><br>
                <transition
                  @before-enter="beforeEnter"
                  @enter="enter"
                  @after-enter="afterEnter"
                  @enter-cancelled="enterCancelled"

                  @before-leave="beforeLeave"
                  @leave="leave"
                  @after-leave="afterLeave"
                  @leave-cancelled="leaveCancelled"
                  :css="false">
                  <div style="width: 300px; height: 100px; background-color: lightgreen" v-if="load">This is some alert via js</div>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        el: 'button',
        data() {
            return {
              show: false,
              load: true,
              alertAnimation: 'fade',
              elementWidth: 100
            }
        },
        methods: {
          beforeEnter: function (el){
            console.log('beforeEnter')
            this.elementWidth = 100
            el.style.width = this.elementWidth + 'px'
          },
          enter: function (el, done){
            console.log('enter')
            let round = 1
            const interval = setInterval(() => {
              el.style.width = (this.elementWidth + round * 10) + 'px'
              round++
              if (round > 20){
                clearInterval(interval)
                done()
              }
            }, 20)
            done()
          },
          afterEnter: function (el){
            console.log('afterEnter')
          },
          enterCancelled: function (el){
            console.log('enterCancelled')
          },
          beforeLeave: function (el){
            console.log('beforeLeave')
            this.elementWidth = 300
            el.style.width = this.elementWidth + 'px'
          },
          leave: function (el, done){
            console.log('leave')
            let round = 1
            const interval = setInterval(() => {
              el.style.width = (this.elementWidth - round * 10) + 'px'
              round++
              if (round > 20){
                clearInterval(interval)
                done()
              }
            }, 20)
          },
          afterLeave: function (el){
            console.log('afterLeave')
          },
          leaveCancelled: function (el){
            console.log('leaveCancelled')
          }
        }
    }
</script>

<style>
  .fade-enter {
    opacity: 0;
  }
  .fade-enter-active {
    transition: opacity 1s;
  }
  .fade-leave {
    /* opacity: 1; */
  }
  .fade-leave-active {
    transition: opacity 1s;
    opacity: 0;
  }

  .slide-enter {
    opacity: 0;
  }
  .slide-enter-active {
    animation: slide-in 1s ease-out forwards;
    transition: opacity 1s;
  }
  .slide-leave {
  }
  .slide-leave-active {
    animation: slide-out 3s ease-out forwards;
    transition: opacity 1s;
    opacity: 0;
  }

  @keyframes slide-in {
    from {
      transform: translateY(20px);
    }
    to {
      transform: translateY(0);
    }
  }
  @keyframes slide-out {
    from {
      transform: translateY(0);
    }
    to {
      transform: translateY(20px);
    }
  }

</style>
