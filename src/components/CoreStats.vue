<template>
  <div class="stat-sheet__core-stats">
    <table class="stat-sheet">
      <tbody class="core-stats-table">
        <tr class="tr-head">
          <td>HP</td>
          <td>
            <input type="text" readonly v-model="getHpValue">
          </td>
        </tr>
        <tr class="tr-head">
          <td>Stamina</td>
          <td>
            <input type="text" readonly v-model="getStaminaValue">
          </td>
        </tr>
        <tr class="tr-head">
          <td>Equip Load</td>
          <td>
            <input type="text" readonly v-model="getEquipBurdenValue">
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  name: 'core-stats',
  props: {
    characterBuildEndurance: {
      type: Number,
      required: true
    },
    characterBuildVitality: {
      type: Number,
      required: true
    },
  },
  data: () => ({
    coreStats: {},
    hpValues: { 
      8:531,9:552,10:573,11:594,12:616,13:638,14:659,15:682,16:698,17:719,18:742,19:767,20:793,21:821,22:849,23:878,24:908,25:938,26:970,27:1001,28:1034,29:1066,30:1100,31:1123,32:1147,33:1170,34:1193,35:1216,36:1239,37:1261,38:1283,39:1304,40:1325,41:1346,42:1366,43:1386,44:1405,45:1424,46:1442,47:1458,48:1474,49:1489,50:1500,51:1508,52:1517,53:1526,54:1535,55:1544,56:1553,57:1562,58:1571,59:1580,60:1588,61:1597,62:1606,63:1615,64:1623,65:1632,66:1641,67:1649,68:1658,69:1666,70:1675,71:1683,72:1692,73:1700,74:1709,75:1717,76:1725,77:1734,78:1742,79:1750,80:1758,81:1767,82:1775,83:1783,84:1791,85:1799,86:1807,87:1814,88:1822,89:1830,90:1837,91:1845,92:1852,93:1860,94:1867,95:1874,96:1881,97:1888,98:1894,99:1900
    },
    staminaValuesTable: [
      88,90,91,93,95,97,98,100,102,104,106,108,110,112,115,117,119,121,124,126,129,131,133,136,139,141,144,146,149,152,154,157,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160,160
    ],
  }),
  computed: {
    getHpValue() {
      return this.hpValues[this.coreStats.hp]
    },
    getStaminaValue() {
      return this.staminaValuesTable[this.coreStats.endurance - 7]
    },
    getEquipBurdenValue() {
      return (40 + this.coreStats.endurance).toFixed(1)
    }
  },
  watch: {
    characterBuildVitality: {
      handler(newVal) {
        this.coreStats.hp = newVal
      },
      deep: true
    },
    characterBuildEndurance: {
      handler(newVal) {
        this.coreStats.endurance = newVal
      },
      deep: true
    },
  },
  methods: {
  },
  mounted() {
    this.coreStats.hp = this.characterBuildVitality
    this.coreStats.endurance = this.characterBuildEndurance
  }
}

</script>

<style lang="scss">
.stat-sheet {
  &__core-stats {
    padding-bottom: .5em;
  }
}
table.stat-sheet {
  display: block;
}
.core-stats-table {
  display: flex;
  flex-direction: column;
  align-content: flex-start;
  width: 100%;
  tr {
    display: flex;
    flex: 1;
    justify-content: space-between;
  }
  input {
    
  }
}
</style>