<template>
  <div class="dark-souls-character-planner container">
    <div class="dark-souls-character-planner__class ">
      <h1>Class</h1>
      <div>
        <!-- <Classes @select-class="setNewClass"></Classes> -->
        <select id="class-selector" @change="setNewClass" v-model="characterClass">
          <option v-for="(obj, key) in classes" :key="key" :value="obj" v-text="obj.level + ' - ' + obj.name"></option>
        </select>
      </div>
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
                <input type="text" v-model="characterBuild[obj.name]">
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
    <Defence :characterStats="characterBuild"></Defence>
  </div>
</template>

<script>
//import Classes from "../components/ClassPicker"
import Defence from "../components/Defences"

export default {
  name: 'stat-sheet',
  components: { Defence},
  props: {},
  data: () => ({
    loading: false,
    error: '',
    classes: [
      { name: "Warrior", level: 4, vitality: 11, attunement: 8, endurance: 12, strength: 13, dexterity: 13, resistance: 11, intelligence: 9, faith: 9 },
      { name: "Knight", level: 5, vitality: 14, attunement: 10, endurance: 10, strength: 11, dexterity: 11, resistance: 10, intelligence: 9, faith: 11  },
      { name: "Wanderer", level: 3, vitality: 10, attunement: 8, endurance: 12, strength: 13, dexterity: 13, resistance: 11, intelligence: 9, faith: 9  },
      { name: "Thief", level: 5, vitality: 9, attunement: 11, endurance: 9, strength: 9, dexterity: 15, resistance: 10, intelligence: 12, faith: 11  },
      { name: "Bandit", level: 6, vitality: 12, attunement: 8, endurance: 14, strength: 14, dexterity: 9, resistance: 11, intelligence: 8, faith: 10 },
      { name: "Hunter", level: 4, vitality: 11, attunement: 9, endurance: 11, strength: 12, dexterity: 14, resistance: 11, intelligence: 9, faith: 9 },
      { name: "Sorcerer", level: 3, vitality: 8, attunement: 15, endurance: 8, strength: 9, dexterity: 11, resistance: 8, intelligence: 15, faith: 8  },
      { name: "Pyromancer", level: 1, vitality: 10, attunement: 12, endurance: 11, strength: 12, dexterity: 9, resistance: 12, intelligence: 12, faith: 8 },
      { name: "Cleric", level: 2, vitality: 11, attunement: 11, endurance: 9, strength: 12, dexterity: 8, resistance: 11, intelligence: 8, faith: 14 },
      { name: "Deprived", level: 6, vitality: 11, attunement: 11, endurance: 11, strength: 11, dexterity: 11, resistance: 11, intelligence: 11, faith: 11 }
    ],
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
    lastCharacterLevel : null,
    nextLevelSouls: 0,
    totalSoulsSpent: 0,
    lastSoulsSpent: 0,
  }),
  computed: {
    nextSoulLevelCost() {
      const soulLevel = this.characterBuild.level
      //console.log(soulLevel)
      let soulsRequired
      let prevSoulsRequired

      //Caclulate the number of souls Needed to Level up from current Level based upon before 12 and after 12 calculcations
      //Formula obtained from http://darksouls.wikidot.com/soul-level
      if (soulLevel < 12) {
        soulsRequired = Math.round((0.0068 * soulLevel ** 3) - (0.06 * soulLevel ** 2) + (17.1 * soulLevel) + 639)
        prevSoulsRequired = Math.round((0.0068 * this.lastCharacterLevel ** 3) - (0.06 * this.lastCharacterLevel ** 2) + (17.1 * this.lastCharacterLevel) + 639)
      } else {
        soulsRequired = Math.round(((0.02 * soulLevel ** 3) + (3.06 * soulLevel ** 2) + (105.6 * soulLevel)) - 895)
        prevSoulsRequired = Math.round(((0.02 * this.lastCharacterLevel ** 3) + (3.06 * this.lastCharacterLevel ** 2) + (105.6 * this.lastCharacterLevel)) - 895)
        if (soulLevel == 12) prevSoulsRequired = Math.round((0.0068 * this.lastCharacterLevel ** 3) - (0.06 * this.lastCharacterLevel ** 2) + (17.1 * this.lastCharacterLevel) + 639)
      } 
      // console.log(`current souls required are ${soulsRequired}`)
      // console.log(`The previous souls required were ${prevSoulsRequired}`)

      if (soulLevel === this.lastCharacterLevel) {
        return soulsRequired
      } else if (soulLevel > this.lastCharacterLevel) {
        //Add previous souls required to the total the total souls spent
        this.addTotalSouls(prevSoulsRequired)
      } else if (soulLevel < this.lastCharacterLevel) {
        //Subtract souls required from the total souls spent
        this.subtractTotalSouls(soulsRequired)
      }
      return soulsRequired
      //return 0
    },
  },
  methods: {
    setNewClass() {
      //Need to check if stats are changed then just adjust for new base class
      this.characterBuild = {...this.characterClass}
      this.soulsRequired = 0
      this.lastSoulsSpend = 0
    },
    levelUpStat(stat) {
      if (this.characterBuild[stat] && this.characterBuild[stat] < 99) {
        this.characterBuild[stat] = this.characterBuild[stat] + 1
        this.lastCharacterLevel = this.characterBuild.level
        this.characterBuild.level += 1
      }
    },
    levelDownStat(stat) {
      if (this.characterBuild[stat] && this.characterBuild[stat] - 1 >= this.characterClass[stat]) {
        this.characterBuild[stat] = this.characterBuild[stat] - 1
        this.lastCharacterLevel = this.characterBuild.level
        this.characterBuild.level -= 1
      }
    },
    addTotalSouls(souls) {
      //console.log("got into add")
      if (souls) {
        //console.log(`total souls spent ${this.totalSoulsSpent} plus ${souls}`)
        this.lastSoulsSpent = souls
        this.totalSoulsSpent += souls
      }
    },
    subtractTotalSouls(souls) {
      //console.log("got into subtract")
      if (souls) {
        //console.log(`total souls spent ${this.totalSoulsSpent} minus ${souls}`)
        this.totalSoulsSpent -= souls
        this.lastSoulsSpent = souls
      }
    }
  },
  mounted() {
    let selectClass = document.getElementById('class-selector')
    selectClass.value = this.classes[0]
    this.characterClass = this.classes[0]
    this.characterBuild = {...this.characterClass}
    this.lastCharacterLevel = this.characterBuild.level
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

i {
  cursor: pointer;
}

</style>