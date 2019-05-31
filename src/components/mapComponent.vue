<template>
    <div id="map" @click="fold">
        <div class="walk"></div>
        <div class="left-side">
            <div class="left-near"></div>
            <div class="left-far"></div>
        </div>
        <div class="center-piece">
            <div class="departments">
                <div class="department" v-for="department in departments" @click="$router.push(department.url)">
                    <img src="../assets/nametag.png" alt="" class="img-fluid">
                    <span class="deptName">{{ department.name }} </span>
                </div>
            </div>
            <div class="top-side"></div>
            <div class="bottom-side"></div>
        </div>
        <div class="right-side">
            <div class="right-near"></div>
            <div class="right-far"></div>
        </div>
        <div class="text">
            <div class="first-line">I solemnly swear that</div>
            <div class="second-line">I am upto no good</div>
        </div>
        <div class="info">Click to open/close the map</div>
    </div>
</template>

<script>
  export default {
    name: "mapComponent",
    data() {
      return {
        folded: true,
        t2: null,
        t1: null,
        departments: [
          {
            name: "Builders Of Azkaban",
            url: 'boa'
          },
          {
            name: "Automotive Philosophers",
            url: 'automotivePhilosophers'
          },
          {
            name: "Chamber of Coders",
            url: 'chamberOfCoders'
          },
          {
            name: "Half Wave Prince",
            url: 'halfWavePrince'
          },
          {
            name: 'Goblet of Workshops',
            url: 'gobletOfWorkshops'
          },
          {
            name: "Scamander\'s Suitcase",
            url: 'scamandersSuitcase'
          },
          {
            name: "M. A. D. Hollows",
            url: 'madHollows'
          },
          {
            name: "Order of Ohms",
            url: 'orderOfOhms'
          },
        ]
      }
    },
    methods: {
      fold() {
        if(this.folded) {
          this.t2.paused(true)
          this.t1.restart()
          this.folded = false
        }
        else {
          this.t1.reverse()
          this.t2.paused(false)
          this.folded = true
        }
      }
    },
    mounted() {

      this.t1 = new this.$gsap.TimelineMax({
        paused: true
      })

      this.t1.to('.info, .text', 0.1, {
        autoAlpha: 0
      })
      this.t1.to('.left-far', 1.5, {
        rotationY: 180,
        transformOrigin: 'left',
        backgroundImage: "url('" + require('../assets/6.png') + "')"
      })

      this.t1.to('.right-far', 1.5, {
        rotationY: 180,
        transformOrigin: 'right',
        backgroundImage: "url('" + require('../assets/11.png') + "')"
      }, 0)

      this.t1.to('.left-far', 0.5, {
        x: '-100%',
      })


      this.t1.to('.right-far', 0.5, {
        x: '100%'
      }, 1.5)

      this.t1.from('.right-near, .left-near', 0.5, {
        autoAlpha: 0
      }, 1.5)

      this.t1.to('.top-side', 0.5, {
        rotationX: 180,
        transformOrigin: "top left"
      })

      this.t1.to('.bottom-side', 0.5, {
        rotationX: 180,
        transformOrigin: "bottom left"
      }, "-=0.5")

      this.t1.from('.walk, .departments', 0.5, {
        autoAlpha: 0
      })



      /*LETTER ANIMATION*/


      this.t2 = new this.$gsap.TimelineMax({
        repeat: -1,
        yoyo: true
      })

      let t3 = new this.$gsap.TimelineMax({})


      Array.from(document.querySelector('.text').children, (line)=> {
        let letters = line.innerHTML.split("")
        let blockLetters = []
        letters.forEach((letter) => {
          if(letter === " ")
            blockLetters.push("<div class=\"letter\"> &nbsp; </div>")
          else
            blockLetters.push("<div class=\"letter\">" + letter + "</div>")
        })
        line.innerHTML = blockLetters.join("")
      })

      let letters = document.querySelectorAll('.letter')
      letters.forEach(function(letter) {
        letter.style.display = 'inline-block'
      })

      t3.staggerFrom('.letter', 0.5, {
        autoAlpha: 0
      }, 0.1)

      t3.from('.info', 0.5, {
        scale: 1.5,
        autoAlpha: 0
      })

      this.t2.staggerTo(".letter", 0.5, {
        scale: 1.2
      }, 0.1)

      this.t2.staggerTo(".letter", 0.5, {
        scale: 1
      }, 0.1, 0)
    }
  }
</script>

<style scoped lang="sass">
@import ../sass/mapComponent
</style>