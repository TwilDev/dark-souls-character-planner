<template>
  <div class="matchmaking-stats">
    <ul>
      <li>
        <span>Invasion Orbs</span>
        <div>
          <label for="upper-level">Upper Limit</label>
          <h5 class="upper-limit" v-text="eyeInvasion.upper"></h5>
        </div>
        <div>
          <label for="upper-level">Lower Limit</label>
          <h5 class="upper-limit" v-text="eyeInvasion.lower > 0 ? eyeInvasion.lower : 1"></h5>
        </div>
      </li>
      <li>
        <span>Summon Signs</span>
        <div>
          <label for="upper-level">Upper Limit</label>
          <h5 class="upper-limit" v-text="summonSign.upper"></h5>
        </div>
        <div>
          <label for="upper-level">Lower Limit</label>
          <h5 class="upper-limit" v-text="summonSign.lower > 0 ? summonSign.lower : 1"></h5>
        </div>
      </li>
      <li>
        <span>Covenant Invasions</span>
        <div>
          <label for="upper-level">Upper Limit</label>
          <h5 class="upper-limit" v-text="covenantInvasion.upper"></h5>
          <label for="upper-level">Lower Limit</label>
          <h5 class="upper-limit" v-text="covenantInvasion.lower > 0 ? covenantInvasion.lower : 1"></h5>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'player-matchmaking',
  props: {
    characterLevel: {
      type: Number,
      required: true
    },
  },
  data: () => ({
    eyeInvasion: {},
    summonSign: {},
    covenantInvasion: {},
  }),
  computed: {},
  watch: {
    characterLevel: {
      handler(newVal, oldVal) {
        if (newVal !== oldVal) {
          let soulLevel = newVal
          this.eyeInvasion.upper = Math.floor(soulLevel + (20 + 0.1 * soulLevel)) > 715 ? 715 : Math.floor(soulLevel + (20 + 0.1 * soulLevel))
          this.eyeInvasion.lower = Math.floor(soulLevel - (0.1 * soulLevel)) > 715 ? 715 : Math.floor(soulLevel - (0.1 * soulLevel))

          this.summonSign.upper = Math.floor(soulLevel + (10 + 0.1 * soulLevel)) > 715 ? 715 : Math.floor(soulLevel + (10 + 0.1 * soulLevel))
          this.summonSign.lower = Math.floor(soulLevel - (10 + 0.1 * soulLevel)) > 715 ? 715 : Math.floor(soulLevel - (10 + 0.1 * soulLevel))

          this.covenantInvasion.upper = Math.floor(soulLevel + (0.1 * soulLevel)) > 715 ? 715 : Math.floor(soulLevel + (0.1 * soulLevel))
          this.covenantInvasion.lower = Math.floor(soulLevel - (20 + 0.2 * soulLevel)) > 715 ? 715 : Math.floor(soulLevel - (20 + 0.2 * soulLevel))
        }
      },
      deep: true
    }
  },
  methods: {
    
  }
}

</script>