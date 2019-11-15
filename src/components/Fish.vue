<template>
  <div v-bind:style="fishStyle">
    <img src="@/assets/think_fish.png/" v-bind:style="fishImageStyle" />
  </div>
</template>

<script>
  const FISH_WIDTH = 250
  const FISH_HEIGHT = 200

  export default {
    props: {
      fishProps: Object,
      speed: Number
    },
    data() {
      return {
        posX: 0,
        posY: 0,
        fish_speed: this.speed,
        changeX: 3,
        changeY: 3,
        fishStyle: {
          display: 'flex',
          justifyContent: 'center',
          alignItems: 'center',
          width: `${FISH_WIDTH}px`,
          height: `${FISH_HEIGHT}px`,
          transform: 'translate(0px, 0px)',
          willChange: 'transform'
        },
        fishImageStyle: {
          width: `${FISH_WIDTH - 20}px`,
          height: `${FISH_HEIGHT - 20}px`,
          transform: `rotateY(${180}deg)`
        }
      }
    },
    methods: {
      animateFish() {
        this.posX += this.changeX * (this.speed / 2)
        this.posY += this.changeY * (this.speed / 2)

        var isRight = this.posX >= this.fishProps.wrapperWidth - FISH_WIDTH
        var isLeft = this.posX <= 0
        var isTop = this.posY <= 0
        var isBottom = this.posY >= this.fishProps.wrapperHeight - FISH_HEIGHT

        var isHorizontalBoundary = isLeft || isRight
        var isVerticalBounday = isTop || isBottom

        if (isHorizontalBoundary) {
          this.changeX *= -1
        }
        if (isVerticalBounday) {
          this.changeY *= -1
        }

        if (isLeft) {
          this.fishImageStyle.transform = `rotateY(${180}deg)`
        } else if (isRight) {
          this.fishImageStyle.transform = `rotateY(${0}deg)`
        }

        this.fishStyle.transform = `translate(${this.posX}px, ${this.posY}px)`

        requestAnimationFrame(this.animateFish)
      }
    },
    mounted() {
      requestAnimationFrame(this.animateFish)
    }
  }
</script>
