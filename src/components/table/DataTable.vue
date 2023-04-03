<template>
  <table>
    <thead>
      <tr>
        <th v-for="(col, index) in column" :key="index">
          {{ col.field }}
        </th>
        <th v-if="sumColumns.length > 0">{{ this.calculate === total ? 'Total' : 'Average' }}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(row, index) in data" :key="index">
        <td v-for="(col, cIndex) in column" :key="cIndex">
          <template v-if="col.name !== 'actions'">
            <template v-if="!row.editing">{{ row[col.value] }}</template>
            <template v-else>
              <input
                v-if="col.type !== 'boolean'"
                type="text"
                v-model="row[col.value]"
              />
              <input
                v-else
                type="checkbox"
                :label="col.value"
                v-model="row[col.value]"
              />
            </template>
          </template>
          <template v-else>
            <slot name="actions" :row="row" :index="index" />
          </template>
        </td>
        <td v-if="sumColumns.length > 0">
          {{ calculateTotal(row, true) }}
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    column: {
      type: Array,
      default: () => [],
    },
    sumColumns: {
      type: Array,
      default: () => [],
    },
    calculate: {
      type: String,
      default: "sum",
    },
  },
  methods: {
    calculateTotal(row, display = false) {
      let total = 0;
      for (let col of this.sumColumns) {
        total += row[col];
      }
      if (this.calculate === "average") {
        total /= this.sumColumns.length;
      }
      return display ? total : total;
    },
  },
};
</script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

th {
  background-color: #f2f2f2;
}
</style>
