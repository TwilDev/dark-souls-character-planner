<template>
  <div class="dark-souls-character-planner container">
    <div class="dark-souls-character-planner__class ">
      <h1>Class</h1>
      <ClassPicker @select-class="setClass"></ClassPicker>
    </div>
    <div class="dark-souls-character-planner__stat-sheet">
      <div class="d-flex justify-content-center">
        <table class="text-align__left stat-sheet">
          <thead>
            <tr>
              <td></td>
              <td>Starting</td>
              <td>Current</td>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Soul Level</td>
              <td>
                <input type="text" disabled v-model="characterClass.level"/>
              </td>
              <td>
                <input type="text" readonly v-model="characterBuild.level"/>
              </td>
            </tr>
            <tr v-for="(obj, key) in stats" :key="key">
              <td v-text="obj.name"></td>

              <td>
                <input type="text" disabled v-model="characterClass[obj.name]">
              </td>
              <td>
                <input type="text" readonly v-model="characterBuild[obj.name]">
              </td>
              <td class="d-flex">
                <i @click="levelUpStat(obj.name)" class="gg-arrow-up"></i>
                <i @click="levelDownStat(obj.name)" class="gg-arrow-down"></i>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="dark-souls-character-planner__stat-sheet--souls-cost">
        <div class="d-flex justify-content-around">
          <span>Souls to next level</span>
          <span>Total Souls Spent</span>
        </div>
        <div class="d-flex justify-content-around">
          <input type="text" readonly v-model="nextSoulLevelCost"/>
          <input type="text" readonly v-model="totalSoulsSpent"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ClassPicker from "../components/ClassPicker.vue"


export default {
  name: 'stat-sheet',
  components: { ClassPicker },
  props: {},
  data: () => ({
    loading: false,
    error: '',
    stats: [
     { name: "vitality" },
     { name: "attunement" },
     { name: "endurance" },
     { name: "strength" },
     { name: "dexterity"},
     { name: "resistance"},
     { name: "intelligence"},
     { name: "faith"}
    ],
    characterClass : {},
    characterBuild : {},
    nextLevelSouls: 0,
    totalSoulsSpent: 0,
    lastSoulsSpent: 0
  }),
  computed: {
    nextSoulLevelCost() {
      const x = this.characterBuild.level
      if (x < 12) {
        let soulsRequired = Math.round((0.0068 * x ** 3) - (0.06 * x ** 2) + (17.1 * x) + 639)
        this.addTotalSouls(soulsRequired)
        return soulsRequired
      } else {
       let soulsRequired = Math.round(((0.02 * x ** 3) + (3.06 * x ** 2) + (105.6 * x)) - 895)
       this.addTotalSouls(soulsRequired)
        return soulsRequired
      }
    }
  },
  methods: {
    setClass(selectedClass) {
      this.characterClass = Object.create(selectedClass)
      this.characterBuild = Object.create(selectedClass)
    },
    levelUpStat(stat) {
      if (this.characterBuild[stat] < 99) {
        this.characterBuild[stat] = this.characterBuild[stat] + 1
        this.characterBuild.level += 1
      }
    },
    levelDownStat(stat) {
      if (this.characterBuild[stat] - 1 >= this.characterClass[stat]) {
        this.characterBuild[stat] = this.characterBuild[stat] - 1
        this.characterBuild.level -= 1
      }
    },
    addTotalSouls(souls) {
      console.log(souls)
      if (souls) {
         this.totalSoulsSpent += souls
      }
     
    }
  }
}

</script>

<style lang="scss">

.dark-souls-character-planner {
  &__stat-sheet {
    &--souls-cost {
      width: 25%;
      margin: auto;
      padding-top: 1em;

      span {
        font-size: 11px;
        padding-bottom: .4em
      }
      input {
        width: 120px;
      };
    }
  }
}

</style>