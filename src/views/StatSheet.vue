<template>
  <div class="dark-souls-character-planner container">
    <div class="dark-souls-character-planner__class ">
      <h1>Dark Souls (ダークソウル) Character Builder</h1>
      <h2>Class</h2>
      <div>
        <!-- <Classes @select-class="setNewClass"></Classes> -->
        <select id="class-selector" @change="setNewClass" v-model="characterClass">
          <option v-for="(obj, key) in classes" :key="key" :value="obj" v-text="obj.level + ' - ' + obj.name"></option>
        </select>
      </div>
    </div>
    <div class="dark-souls-character-planner__wrapper">
      <div class="dark-souls-character-planner__stat-sheet character-planner_section">
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
                  <!-- <input type="text" @change="onTestChange" v-model.lazy="characterBuild[obj.name]"> -->
                  <input type="text" :id="obj.name" @change="onManualStatChange(characterBuild[obj.name], obj.name, $event)" :value="characterBuild[obj.name]">
                </td>
                <td class="d-flex">
                  <i @click="levelDownStat(obj.name)" class="gg-arrow-down"></i>
                  <i @click="levelUpStat(obj.name)" class="gg-arrow-up"></i>
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
            <input type="text" readonly v-model="nextLevelSouls"/>
            <input type="text" readonly v-model="totalSoulsSpent"/>
          </div>
        </div>
        <Matchmaking :characterLevel="characterBuild.level"></Matchmaking>
      </div>
      <div class="character-planner_section">
        <CoreStats :characterBuildVitality="characterBuild.vitality" :characterBuildEndurance="characterBuild.endurance"></CoreStats>
        <Defence :characterStats="characterBuild"></Defence>
      </div>
    </div>


    
  </div>
</template>

<script>

//import Classes from "../components/ClassPicker"
import Defence from "../components/Defences"
import Matchmaking from "../components/Matchmaking"
import CoreStats from "../components/CoreStats"

export default {
  name: 'stat-sheet',
  components: { Defence, Matchmaking, CoreStats },
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
    test: {},
  }),
  computed: {
  },
  methods: {
    setNewClass() {
      //Need to check if stats are changed then just adjust for new base class
      this.characterBuild = {...this.characterClass}
      this.soulsRequired = 0
      this.lastSoulsSpend = 0
    },
    levelUpStat(stat) {
      if (this.loading) return
      if (this.characterBuild[stat] && this.characterBuild[stat] < 99) {
        this.characterBuild[stat] = this.characterBuild[stat] + 1
        this.lastCharacterLevel = this.characterBuild.level
        this.characterBuild.level += 1
        //this.calculateSoullevelCost(this.characterBuild.level)
        this.calculateSoulLevelCostJump(this.lastCharacterLevel, this.characterBuild.level)
      }
    },
    levelDownStat(stat) {
      if (this.loading) return
      if (this.characterBuild[stat] && this.characterBuild[stat] - 1 >= this.characterClass[stat]) {
        this.characterBuild[stat] = this.characterBuild[stat] - 1
        this.lastCharacterLevel = this.characterBuild.level
        this.characterBuild.level -= 1
        //this.calculateSoullevelCost(this.characterBuild.level)
        this.calculateSoulLevelCostJump(this.lastCharacterLevel, this.characterBuild.level)
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
        console.log(souls)
        this.totalSoulsSpent -= souls
        this.lastSoulsSpent = souls
      }
    },
    onManualStatChange(stat, statName, e) {
      //Check new event not null or not equal to current stat
      if (!e.target.value || parseInt(e.target.value) == this.characterBuild[statName] ) {
        let input = document.getElementById(statName)
        input.value = stat
        return
      }
  
      let newStatValue = parseInt(e.target.value)

      //Check if altered stat is below the base class level minumum
      if (newStatValue < this.characterClass[statName]) {
        newStatValue = this.characterClass[statName]
        let input = document.getElementById(statName)
        input.value = newStatValue
      }

      //Get Difference and new soul Level from difference
      let statDifference = newStatValue - this.characterBuild[statName]
      
      //Set last character level
      this.lastCharacterLevel = this.characterBuild.level

      let newSoulLevel = this.characterBuild.level += (statDifference)
      //assign new values
      this.characterBuild.level = newSoulLevel
      this.characterBuild[statName] = newStatValue
      this.calculateSoulLevelCostJump(this.lastCharacterLevel, this.characterBuild.level)
      //this.calculateSoullevelCost(this.characterBuild.level)
    },
    calculateSoullevelCost(soulLevel) {
      //console.log(soulLevel)
      let soulsRequired
      let prevSoulsRequired

      //Caclulate the number of souls Needed to Level up from current Level based upon before 12 and after 12 calculcations
      //Formula obtained from http://darksouls.wikidot.com/soul-level
      if (soulLevel < 12) {
        soulsRequired = Math.round((0.0068 * soulLevel ** 3) - (0.06 * soulLevel ** 2) + (17.1 * soulLevel) + 639)
        prevSoulsRequired = Math.round((0.0068 * this.lastCharacterLevel ** 3) - (0.06 * this.lastCharacterLevel ** 2) + (17.1 * this.lastCharacterLevel) + 639)
      } else {
        soulLevel += 1
        soulsRequired = Math.round(((0.02 * soulLevel ** 3) + (3.06 * soulLevel ** 2) + (105.6 * soulLevel)) - 895)
        prevSoulsRequired = Math.round(((0.02 * this.lastCharacterLevel ** 3) + (3.06 * this.lastCharacterLevel ** 2) + (105.6 * this.lastCharacterLevel)) - 895)
        //if (soulLevel == 12) prevSoulsRequired = Math.round((0.0068 * this.lastCharacterLevel ** 3) - (0.06 * this.lastCharacterLevel ** 2) + (17.1 * this.lastCharacterLevel) + 639)
        if (soulLevel === 13) {
          prevSoulsRequired = Math.round((0.0068 * 12 ** 3) - (0.06 * 12 ** 2) + (17.1 * 12) + 639)
        }
      
      } 

      if (soulLevel === this.lastCharacterLevel) {
        this.nextLevelSouls = soulsRequired
      } else if (soulLevel > this.lastCharacterLevel) {
        //Add previous souls required to the total the total souls spent
        this.addTotalSouls(prevSoulsRequired)
      } else if (soulLevel < this.lastCharacterLevel) {
        //Subtract souls required from the total souls spent
        this.subtractTotalSouls(soulsRequired)
      }
      this.nextLevelSouls = soulsRequired
      //return 0
    },
    calculateSoulLevelCostJump(oldSl, newSl) {
      //Make a sum variable
      //Difference variable that shows whether different between new and old is positive or negative
      //use oldSL and newSL as indexes in a for loop
      this.loading = true

      let lvlUpValues = []
      //Level UP cost
      if (oldSl < newSl) {
        for (let i=oldSl; i<newSl; i++) {
          if (i < 12) {
            let soulsRequired = Math.round((0.0068 * i ** 3) - (0.06 * i ** 2) + (17.1 * i) + 639)
            lvlUpValues.push(soulsRequired)
          } else {
            let soulsRequired = Math.round(((0.02 * i ** 3) + (3.06 * i ** 2) + (105.6 * i)) - 895)
            lvlUpValues.push(soulsRequired)
          }
        }
        const sum = lvlUpValues.reduce((a, b) => a + b, 0)
        this.totalSoulsSpent += sum
      }
      //Level DOWN cost
      if (oldSl > newSl) {
        for (let i=oldSl - 1; i >= newSl; i-- ) {
          if (i < 12) {
            let soulsRequired = Math.round((0.0068 * i ** 3) - (0.06 * i ** 2) + (17.1 * i) + 639)
            lvlUpValues.push(soulsRequired)
          } else {
            let soulsRequired = Math.round(((0.02 * i ** 3) + (3.06 * i ** 2) + (105.6 * i)) - 895)
            lvlUpValues.push(soulsRequired)
          }
          
        }
        const sum = lvlUpValues.reduce((a, b) => a + b, 0)
        this.totalSoulsSpent -= sum
      }
      this.loading = false
    }
  },
  mounted() {
    let selectClass = document.getElementById('class-selector')
    selectClass.value = this.classes[0]
    this.characterClass = this.classes[0]
    this.characterBuild = {...this.characterClass}
    this.lastCharacterLevel = this.characterBuild.level
    this.calculateSoullevelCost(this.characterBuild.level)
  }
}

</script>

<style lang="scss">

.dark-souls-character-planner {
  &__wrapper {
    display: flex;
  }
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

.character-planner_section {
  padding: 1rem;
}

i {
  cursor: pointer;
}

</style>