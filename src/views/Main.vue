<template>
    <div id="main">
        <section>
            <div id="landing">
                <div class="pin-scene">
                    <div class="bird-container bird-container--one">
                        <div class="bird bird--one"></div>
                    </div>

                    <div class="bird-container bird-container--two">
                        <div class="bird bird--two"></div>
                    </div>

                    <div class="bird-container bird-container--three">
                        <div class="bird bird--three"></div>
                    </div>

                    <div class="bird-container bird-container--four">
                        <div class="bird bird--four"></div>
                    </div>

                    <div class="bg-image"></div>
                    <div class="udaan-logo">
                        <img src="../assets/brijeshlogo1.png" alt="udaanLogo" class="img-fluid">
                    </div>
                    <div class="mouse">
                        <div class="mouse-icon">
                            <span class="mouse-wheel"></span>
                        </div>
                    </div>



                    <!--<div class="quidditch-ball"></div> -->
                    <!--<div class="demantadors">-->
                    <!--<div class="demantador">-->
                    <!--<ul>-->
                    <!--<li></li>-->
                    <!--<li></li>-->
                    <!--<li></li>-->
                    <!--<li></li>-->
                    <!--</ul>-->
                    <!--</div>-->
                    <!--</div>-->
                    <!--<div class="coming-soon">Coming soon</div> -->




                </div>
            </div>
        </section>
        <section>
            <div id="about">
                <aboutComponent class="aboutComponent"></aboutComponent>
                <div class="particles">
                    <div class="particle" v-for="n in 50"></div>
                </div>
            </div>
        </section>
        <section>
            <mapComponent></mapComponent>
        </section>
    </div>
</template>

<script>
  import aboutComponent from '../components/aboutComponent'
  import mapComponent from '../components/mapComponent'




  export default {
    name: "Main",
    components: {
      aboutComponent,
      mapComponent,
    },
    mounted() {



      //    COMING SOON ANIMATION



      /*let t2 = new this.$gsap.TimelineMax({
        repeat: -1,
        yoyo: true
      })

      let line = document.querySelector('.coming-soon')
      let letters = line.innerHTML.split("")
      let blockLetters = []
      letters.forEach((letter) => {
        if(letter === " ")
          blockLetters.push("<div class=\"letter\">&thinsp;</div>")
        else
          blockLetters.push("<div class=\"letter\">" + letter + "</div>")
      })
      line.innerHTML = blockLetters.join("")

      document.querySelectorAll(".letter").forEach(function(el) {
        el.style.display = "inline-block"
      })

      t2.staggerTo(".letter", 1.5, {
        scale: 1.2,
        y: -10
      }, 0.1)

      t2.staggerTo(".letter", 1, {
        scale: 1,
        y: 0
      }, 0.1, 0)
*/


      //LANDING COMPONENT ANIMATIONS
      let t1 = new this.$gsap.TimelineMax()
      t1.from('.bg-image', 0.5, {
        scale: 1.5,
        autoAlpha: 0,
        ease: Power1.easeOut
      })

      let controller = new this.$scrollmagic.Controller()

      //LANDING COMPONENT SCROLL
      let landingScrollTl = new this.$gsap.TimelineMax().add([
        TweenMax.to('#landing .heading', 4, {
          autoAlpha: 0,
          scale: 2,
          y: 100
        }),
        TweenMax.to('.bg-image, .coming-soon', 4, {
          scale: 1.5
        }),
        TweenMax.to('.demantador', 4, {
          x: 100,
          scale: 0.5,
          autoAlpha: 0
        }),
        TweenMax.to('.udaan-logo, .mouse', 4, {
          y: -50,
          scale: 0.5,
          autoAlpha: 0
        })
      ])

      let scrollLanding = new this.$scrollmagic.Scene({
        triggerElement: '.pin-scene',
        triggerHook: 0,
        duration: '110%'
      })
        .setTween(landingScrollTl)
        .setPin('.pin-scene')
        .addTo(controller)

      //  ABOUT COMPONENT SCROLL

      let aboutScrollTl = new this.$gsap.TimelineMax().add([
        TweenMax.to('.bg-image', 4, {
          autoAlpha: 0
        }),
        TweenMax.staggerTo('.particle', 16, {
          cycle: {
            x: function (i) {
              if (i % 2 === 0)
                return (Math.random() * (-400) + 1)
              else
                return (Math.random() * (400) + 1)
            },
            y: function (i) {
              if (i % 2 === 0)
                return (Math.random() * (-400) + 1)
              else
                return (Math.random() * (400) + 1)
            },
            scale: function () {
              return Math.random() * 5
            },
            rotation: function () {
              return Math.random() * 360
            },
            backgroundColor: function () {
              return 'rgba(' + Math.round(Math.random() * 255) + ',' + Math.round(Math.random() * 255) + ',' + Math.round(Math.random() * 255) + ')'
            }
          },
          autoAlpha: 0,
          display: "none"
        }, 0.4),
        TweenMax.from('#about', 4, {
          autoAlpha: 0
        }),
        TweenMax.from('.aboutComponent', 8, {
          autoAlpha: 0
        }),
        TweenMax.from('.title, .sub-title, .center-headline, .footer-headline', 8, {
          scale: 0
        }),
        TweenMax.from('.article', 8, {
          scaleY: 0
        }, "+=2"),
        TweenMax.from('.center-gif', 8, {
          autoAlpha: 0,
          y: 100
        }),
        TweenMax.staggerFrom('.social-icon', 8, {
          scale: 0
        }, 2)
      ])

      let scrollAbout = new this.$scrollmagic.Scene({
        triggerHook: 0,
        triggerElement: '#about',
        duration: '50%'
      })
        .setTween(aboutScrollTl)
        .setPin('#about')
        .addTo(controller)

    }
  }
</script>

<style scoped lang="sass">
  @import ../sass/main
  @font-face
    font-family: 'dumbledore'
    src: url("../assets/dum1.ttf")

  /*.coming-soon
      position: absolute
      top: 50px
      left: 50%
      z-index: 3
      transform: translateX(-50%)
      color: black
      text-align: center
      font-family: dumbledore, sans-serif
      font-size: 72px
      .letter
          display: inline-block !important*/
</style>