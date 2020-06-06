<template>
  <div class="container">
    <table>
      <thead>
        <tr>
          <th v-for="col in tcolumn" :key="col.id">{{col}}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="row in actors" :key="row.id">
          <td v-for="col in tcolumn" :key="col.id">{{row[col]}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  components: {
    QueryMessage
  },

  name: "ActorsSearch",
  data() {
    return {
      tcolumn: [],
      actors: [],
      actorsData: []
    };
  },

  props: {},

  created() {
    this.fetchActors();
    this.fillActors();
    this.tcolumn = Object.keys(this.actors[0]);
  },

  methods: {
    fetchActors() {
      fetch("/list/actor")
        .then(res => res.json())
        .then(res => {
          this.actorsData = res;
          console.log(this.actorsData);
        });
    },
    fillActors() {
      this.actors = [];
      this.actorsData.forEach(element => {
        let actor = { id: element.id, name: element.name };
        this.actors.push(actor);
      });
    }
  }
};
</script>

<style scoped>
table {
  font-family: "Open Sans", sans-serif;
  width: 750px;
  border-collapse: collapse;
  border: 3px solid #44475c;
  margin: 10px 10px 0 10px;
}

table th {
  text-transform: uppercase;
  text-align: left;
  background: #44475c;
  color: #fff;
  padding: 8px;
  min-width: 30px;
}

table td {
  text-align: left;
  padding: 8px;
  border-right: 2px solid #7d82a8;
}
table td:last-child {
  border-right: none;
}
table tbody tr:nth-child(2n) td {
  background: #d4d8f9;
}
</style>
