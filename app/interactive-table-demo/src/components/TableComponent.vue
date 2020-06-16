<template>
  <div class="table-component">
    <table align="center">
      <thead>
        <tr>
          <th v-for="column in columns" :key="column.field">{{ column.label }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="row in rows" :key="row.id">
          <td v-for="column in columns" :key="column.field">{{ row[column.field]}}</td>
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
          id: 1,
          name: "John",
          age: 20,
          createdAt: "",
          score: 0.03343
        },
        {
          id: 2,
          name: "Jane",
          age: 24,
          createdAt: "2011-10-31",
          score: 0.03343
        },
        {
          id: 3,
          name: "Susan",
          age: 16,
          createdAt: "2011-10-30",
          score: 0.3342
        },
        {
          id: 4,
          name: "Chris",
          age: 55,
          createdAt: "2011-10-11",
          score: 0.41571
        },
        {
          id: 5,
          name: "Dan",
          age: 40,
          createdAt: "2011-10-21",
          score: 0.9045
        },
        {
          id: 6,
          name: "John",
          age: 20,
          createdAt: "2011-10-31",
          score: 0.02901
        }
      ]
    };
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
</style>
