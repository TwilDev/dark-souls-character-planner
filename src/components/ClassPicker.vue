<template>
  <div>
    <select id="class-selector" @change="selectClass" v-model="selectedClass">
      <option v-for="(obj, key) in classes" :key="key" :value="obj" v-text="obj.level + ' - ' + obj.name"></option>
    </select>
  </div>
</template>

<script>

export default {
  name: "class-picker",
  components: {},
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
    selectedClass: {},
  }),
  methods: {
    selectClass() {
      const _cls = this.selectedClass
      this.$emit("select-class", _cls)
    }
  },
  mounted() {
    this.$emit("select-class", this.classes[0])
    let el = document.getElementById("class-selector")
    el.value = this.classes[0]
  }
}

</script>