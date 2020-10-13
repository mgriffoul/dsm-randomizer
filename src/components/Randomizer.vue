<template>
  <div>
    <div class="header">
      <div class="title">
        <span class="title-label">Dsm Randomizer</span
        ><span class="copyright">&copy;</span>
      </div>
      <span class="back-line">Who's gonna speak first ... ?</span>
      <button class="randomize-button" @click="attributeOrder">
        <span class="blink_me">RANDOMIZE =></span>
      </button>
    </div>
    <ul>
      <li v-for="player in players" :key="player.id">
        <component v-bind:is="player.component" />
      </li>
    </ul>
  </div>
</template>

<script>
import {
  Charles,
  Ouzzin,
  Christophe,
  William,
  Julien,
  Regis,
  Anthony,
  Mathieu,
  Jimmy,
  Minh,
  Geoffrey,
  Pos,
  Benjamin,
  Serge
} from './players'

export default {
  name: 'Randomizer',
  components: {
    Charles,
    Ouzzin,
    Anthony,
    William,
    Christophe,
    Regis,
    Julien,
    Mathieu,
    Jimmy,
    Minh,
    Geoffrey,
    Pos,
    Benjamin,
    Serge
  },
  data: () => ({
    players: [
      { id: '1', component: Anthony, avatar: 'anthony.png', order: 0 },
      { id: '13', component: Benjamin, avatar: 'benjamin.png' },
      { id: '2', component: Charles, avatar: 'charles.png', order: 0 },
      { id: '3', component: Christophe, avatar: '', order: 0 },
      { id: '4', component: Geoffrey, avatar: '', order: 0 },
      { id: '5', component: Jimmy, avatar: '', order: 0 },
      { id: '6', component: Julien, avatar: '', order: 0 },
      { id: '7', component: Mathieu, avatar: '', order: 0 },
      { id: '8', component: Minh, avatar: 'minh', order: 0 },
      { id: '9', component: Ouzzin, avatar: '', order: 0 },
      { id: '12', component: Pos, avatar: 'Pos.png' },
      { id: '10', component: Regis, avatar: 'regis.png', order: 0 },
      { id: '11', component: William, avatar: 'william.png', order: 0 },
      { id: '14', component: Serge, avatar: 'serge.png', order: 0 }
    ],
    ticksNumber: 15
  }),
  methods: {
    async attributeOrder (i) {
      this.ticksNumber = 1
      setTimeout(
        this.apply, 1000
      )
    },
    apply () {
      this.calculate()
      this.$nextTick(
        () => {
          if (this.ticksNumber <= 120) {
            setTimeout(this.apply, 700 / this.ticksNumber)
          } else {
            return
          }
          this.ticksNumber++
        }
      )
    },
    calculate () {
      const min = Math.ceil(1)
      const max = Math.floor(this.players.length)
      const attributed = []
      while (attributed.length < this.players.length) {
        const current = Math.floor(Math.random() * (max - min + 1)) + min
        if (!attributed.includes(current)) {
          attributed.push(current)
        }
      }
      let count = 0
      this.players.forEach(player => {
        player.order = attributed[count]
        count++
      })
      this.players.sort(this.comparaison)
    },
    comparaison (first, second) {
      return first.order - second.order
    }
  }
}
</script>

<style lang="scss">
@import "src/scss/variables";

.header {
  display: flex;
  flex-direction: column;
  justify-content: center;

  .title {
    align-items: center;
    text-transform: uppercase;
    color: $extra-color;
    font-size: 60px;
    display: flex;

    .copyright {
      font-size: 35px;
      align-self: flex-start;
    }
  }

  .back-line {
    margin-top: $primary-top-space;
    font-size: 20px;
  }
}

img {
  height: 45px;
}

.randomize-button {
  background-color: $extra-color;
  color: $secondary-color;
  height: 40px;
  min-width: 200px;
  margin: $primary-top-space auto 0 auto;
  border: none;
  border-radius: 15px;
}

ul {
  list-style: none;

  .player {
    display: flex;
    margin-top: $secondary-top-space;
    .name {
      font-size: 25px;
      margin-left: $primary-left-space;
    }
  }
}
.blink_me {
  animation: blinker 6s linear infinite;
}

@keyframes blinker {
  50% {
    opacity: 0;
  }
}
</style>
