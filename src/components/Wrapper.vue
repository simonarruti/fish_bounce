<template>
  <div :style="wrapperContainerStyle" class="wrapper_container">
    <div :style="wrapperStyle">
      <fish :fishProps="fishProps" :speed="fish_speed"></fish>
      <div class="controls" v-show="show_controls">
        <h2>Speed</h2>
        <input type="range" :min="1" :max="20" v-model.number="fish_speed">
        <div class="backgrounds_select">
          <h2>Backgrounds</h2>
          <select name="backgrounds" v-model="background">
            <option value="none">None</option>
            <option value="aquarium">Aquarium</option>
            <option value="space">Space</option>
            <option value="dream">Dream café</option>
            <option value="sammo">Sammo</option>
          </select>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Fish from './Fish.vue'

export default {
  components: { Fish },
  data () {
    return {
      fish_speed: 3,
      background: 'none',
      show_controls: false,
      wrapperStyle: {
        width: `${100}vw`,
        height: `${100}vh`
      },
     fishProps: {
        wrapperWidth: window.innerWidth,
        wrapperHeight: window.innerHeight
      }
    }
  },
  computed: {
    wrapperContainerStyle () {
      return {
        display: 'flex',
        flexDirection: 'column',
        justifyContent: 'center',
        alignItems: 'center',
        height: '100%',
        backgroundImage: this.wrapper_background,
        backgroundSize: 'cover'
      }
    },
    wrapper_background () {
      if (this.background !== 'none') {
        return 'url(' + require(`../assets/${this.background}.jpg`) + ')'
      } else {
        return null
      }
    }
  },
  mounted () {
    window.addEventListener("keypress", event => {
      if (event.key === 'h') {
        this.show_controls = !this.show_controls
      }
    })
  }
}
</script>

<style>
  .wrapper_container {
    background-color: #000000
  }
  .controls {
    position: absolute;
    top: 20px;
    right: 30px;
  }
  .controls h2 {
    color: white;
  }
</style>
