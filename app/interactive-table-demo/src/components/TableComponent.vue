<template>
  <div class="table-component">
    <table align="center">
      <thead>
        <tr>
          <th v-for="column in columns" :key="column.field" @click="setEditCell(null, null)">
            <span>{{ column.label }}</span>
            <div class="arrow">
              <img
                :src="selectArrowImg(column.field, 'up')"
                @click="setSortLogic(column.field, 'up')"
              />
              <img
                :src="selectArrowImg(column.field, 'down')"
                @click="setSortLogic(column.field, 'down')"
              />
            </div>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr @click="setEditCell(null, null)">
          <td v-for="column in columns" :key="column.field">
            <input
              class="filter"
              type="text"
              name="filter"
              placeholder="This is filter."
              v-model="filterValue[column.field]"
            />
          </td>
        </tr>
        <tr v-for="row in rowSorted" :key="row.id" v-show="isShowRow(row)">
          <td
            class="value"
            v-for="column in columns"
            :key="column.field"
            @click="setEditCell(row.id, column.field)"
          >
            <span v-if="!isEdit(row.id, column.field)">{{ row[column.field] }}</span>
            <span v-else>
              <input class="value-edit" type="text" v-model="row[column.field]" />
            </span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import UpArrowWhite from "@/assets/arrow/up-arrow-white.png";
import DownArrowWhite from "@/assets/arrow/down-arrow-white.png";
import UpArrowBlue from "@/assets/arrow/up-arrow-blue.png";
import DownArrowBlue from "@/assets/arrow/down-arrow-blue.png";

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
      },
      sortLogic: {
        column: null,
        dir: null
      },
      filterValue: {
        name: "",
        age: "",
        creadtedAt: "",
        score: ""
      }
    };
  },
  computed: {
    rowSorted() {
      const rows = this.rows;
      const sortLogic = this.sortLogic;

      if (sortLogic.column === null || sortLogic.dir === null) {
        return rows;
      } else {
        return rows.sort((a, b) => {
          if (a[sortLogic.column] < b[sortLogic.column]) {
            return sortLogic.dir === "up" ? -1 : 1;
          } else {
            return sortLogic.dir === "up" ? 1 : -1;
          }
        });
      }
    }
  },
  methods: {
    isEdit(id, property) {
      const obj = { id, property };
      return JSON.stringify(obj) === JSON.stringify(this.editCell);
    },
    setEditCell(id, property) {
      this.editCell = { id, property };
    },
    selectArrowImg(column, dir) {
      const obj = { column, dir };
      if (JSON.stringify(obj) === JSON.stringify(this.sortLogic)) {
        return dir === "up" ? UpArrowBlue : DownArrowBlue;
      } else {
        return dir === "up" ? UpArrowWhite : DownArrowWhite;
      }
    },
    setSortLogic(column, dir) {
      this.sortLogic = { column, dir };
    },
    isShowRow(row) {
      const boolList = Object.keys(this.filterValue).map(property => {
        if (this.filterValue[property] === "") {
          return true;
        }

        const value = `${row[property]}`;
        return value.match(this.filterValue[property]);
      });
      return boolList.every(value => value);
    }
  }
};
</script>

<style scoped>
tr {
  height: 48px;
}

thead {
  font-size: 32px;
}

thead tr {
  height: 60px;
}

th {
  width: 360px;
  background-color: #2c3e50;
  color: #ffffff;
}

tbody {
  font-size: 24px;
}

td.value {
  transition: background-color 0.3s, text-decoration 0.3s, font-weight 0.3s;
  cursor: pointer;
}

td.value:hover {
  background-color: #dcdcdc;
  text-decoration: underline;
  font-weight: bold;
}

.value-edit {
  height: 36px;
  width: 180px;
  font-size: 24px;
  padding: 0 8px;
  text-align: center;
}

.arrow {
  float: right;
  margin-right: 12px;
}

.arrow img {
  display: block;
  height: 20px;
  cursor: pointer;
  margin: 2px 0;
}

.filter {
  font-size: 20px;
  height: 32px;
  width: 280px;
  border: #dcdcdc solid 2px;
  padding: 0 8px;
}
</style>
