<template>
  <div class="table_diet">
    <div class="shadow_box">
      <table class="tables">
        <input type="text" class="form-control" v-model="search">
        <tr class="header__body">
          <th v-for="(header, idx) in headers" :class="{ sortable: header.sortable }" @click="sortItems(header.sortable, header.id)" :key="idx">
            <li class="nav-item active">
              <nuxt-link class="nav-link" to="#">
                <div class="arrow-hov"><div class="dess">{{ header.name }}</div> {{ arrow }}</div>
              </nuxt-link>
            </li>
          </th>
        </tr>
        <tr class="table__body" v-for="dessert of dessertsToShow">
          <th v-for="(header, idx) in headers" :key="idx">
              <div class="desert__body">{{ dessert[header.id] }}</div>
          </th>
        </tr>
      </table>
      <select v-model="selected">
        <option>2</option>
        <option>5</option>
        <option>10</option>
      </select>
      <button type="button" class="btn btn-outline-secondary" :class="{active: item === page}" v-for="(item, index) in Math.ceil(desserts.length / +selected)" @click="changePage(item)">{{ item }}</button>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      selected: 2,
      headers: [
        {
          id: 'name',
          name: 'Dessert (100g serving)'
        },
        {
          id: 'calories',
          name: 'Calories',
          sortable: true
        },
        {
          id: 'fat',
          name: 'Fat (g)',
          sortable: true
        },
        {
          id: 'carbs',
          name: 'Carbs (g)',
          sortable: true
        },
        {
          id: 'protein',
          name: 'Protein (g)',
          sortable: true
        },
        {
          id: 'iron',
          name: 'Iron (%)',
          sortable: true
        }
      ],
      dessertsToShow: [],
      search: '',
      sortType: true,
      desserts: [
        {
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          iron: '1%',
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          iron: '1%',
        },
        {
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          iron: '7%',
        },
        {
          name: 'Cupcake',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          iron: '8%',
        },
        {
          name: 'Gingerbread',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          iron: '16%',
        },
        {
          name: 'Jelly bean',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          iron: '0%',
        },
        {
          name: 'Lollipop',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          iron: '2%',
        },
        {
          name: 'Honeycomb',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          iron: '45%',
        },
        {
          name: 'Donut',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          iron: '22%',
        },
        {
          name: 'KitKat',
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          iron: '6%',
        },
      ],
      page: 2,
      arrow: '↑',
    }
  },
  watch: {
    selected: {
      immediate: true,
      handler(val) {
        this.showItems(1, +val)
      }
    },
    search: {
      immediate: true,
      handler(val) {
        this.searchName(val)
      }
    }
  },
  filters: {
    lowercase(value) {
      return value.toLowerCase()
    }
  },
  methods: {
    showItems(page, count) {
      this.page = page
      this.dessertsToShow = this.desserts.slice(+count * (page - 1), +count * page)
    },
    searchName(val) {
      this.dessertsToShow = this.desserts.filter(item => item.name.includes(val))
      if (this.selected !== this.selected) {
      }
    },
    changePage(page) {
      this.showItems(page, +this.selected)
    },
    sortItems(sortable, id) {
      this.sortType = !this.sortType
      console.log(sortable, id)
      if (!sortable) return
      this.desserts.sort((a, b) => {
        this.arrow = this.sortType ? '↓' : '↑'
        return this.sortType ? b[id] - a[id] : a[id] - b[id]
      })
      this.showItems(1, +this.selected)
    },

  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@100&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap');


li {
  list-style-type: none;
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 13px;
  color: darkgray;
}


.arrow-hov {
  color: lightgray;
  display: flex;
  flex-direction: row;
}

th:first-child .arrow-hov:first-child {
  color: white !important;
}



.arrow-hov:hover {
  color: darkgray;
}

ul {
  margin-left: 0;
  margin-top: 0;
  margin-bottom: 0;
  padding-left: 0;
  color: darkgray;
  display: flex;
  justify-content: center;
}


a {
  text-decoration: none;
  color: gray;
}

a:hover {
  text-decoration: none;
  color: black;
}

.dess {
  color: darkgray;
  padding-right: 5px;
}



.nav-link {
  font-family: 'Quicksand', sans-serif;
  font-size: 16px;
  display: flex;
  flex-direction: row;
}

.desert__body {
  display: flex;
  justify-content: center;
}

.table__body:hover {
  background-color: honeydew;
}

.tables {
  border: 1px solid whitesmoke;
}

.shadow_box {
  -webkit-box-shadow: 1px 4px 8px 2px rgba(34, 60, 80, 0.2);
  -moz-box-shadow: 1px 4px 8px 2px rgba(34, 60, 80, 0.2);
  box-shadow: 1px 4px 8px 2px rgba(34, 60, 80, 0.2);
}

.table_diet {
  display: flex;
  justify-content: center;
  padding-top: 150px;
}

th {
  padding: 10px 20px;
  color: darkgray;
  font-family: 'Quicksand', sans-serif;
  font-size: 15px;
}

td {
  padding: 7px 36px;
  border-bottom: 1px solid black;
}

td:hover {
  background-color: aliceblue;
  transition: 50ms;
}

button.active {
  background: rebeccapurple;
}

th.sortable {
  background: lightgray;
}


</style>
