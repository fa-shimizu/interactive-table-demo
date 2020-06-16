<template>
  <div class="table-component">
    <table align="center">
      <thead>
        <tr>
          <th
            v-for="column in columns"
            :key="column.field"
            @click="setEditCell(null, null)"
          >{{ column.label }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="row in rows" :key="row.id">
          <td
            v-for="column in columns"
            :key="column.field"
            @click="setEditCell(row.id, column.field)"
          >
            <span v-if="!isEdit(row.id, column.field)">{{ row[column.field] }}</span>
            <span v-else>
              <input type="text" v-model="row[column.field]" />
            </span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "table-component",
  data() {
    return {
      columns: [
        {
          label: "Name",
          field: "name"
        },
        {
          label: "Age",
          field: "age"
        },
        {
          label: "Created On",
          field: "createdAt"
        },
        {
          label: "Percent",
          field: "score"
        }
      ],
      rows: [
        {
          id: 0,
          name: "John",
          age: 20,
          createdAt: "",
          score: 0.03343
        },
        {
          id: 1,
          name: "Jane",
          age: 24,
          createdAt: "2011-10-31",
          score: 0.03343
        },
        {
          id: 2,
          name: "Susan",
          age: 16,
          createdAt: "2011-10-30",
          score: 0.3342
        },
        {
          id: 3,
          name: "Chris",
          age: 55,
          createdAt: "2011-10-11",
          score: 0.41571
        },
        {
          id: 4,
          name: "Dan",
          age: 40,
          createdAt: "2011-10-21",
          score: 0.9045
        },
        {
          id: 5,
          name: "John",
          age: 20,
          createdAt: "2011-10-31",
          score: 0.02901
        }
      ],
      editCell: {
        id: null,
        property: null
      }
    };
  },
  methods: {
    isEdit(id, property) {
      const obj = { id, property };
      return JSON.stringify(obj) === JSON.stringify(this.editCell);
    },
    setEditCell(id, property) {
      this.editCell = { id, property };
    }
  }
};
</script>

<style scoped>
tr {
  height: 48px;
}

thead {
  font-size: 36px;
}

thead tr {
  height: 60px;
}

th {
  width: 240px;
}

tbody {
  font-size: 24px;
}

td {
  transition: background-color 0.3s, text-decoration 0.3s, font-weight 0.3s;
  cursor: pointer;
}

td:hover {
  background-color: #dcdcdc;
  text-decoration: underline;
  font-weight: bold;
}

input {
  height: 32px;
  width: 200px;
  font-size: 24px;
  padding: 0 8px;
  text-align: center;
}
</style>
