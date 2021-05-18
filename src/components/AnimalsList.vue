<template>
  <div>
    <h1>
      Animals
    </h1>
    <h4>Add Animal</h4>
    <form @submit.prevent="addAnimal">
      <div>
        <label>
          Species:
        </label>
        <input type="text" v-model="newSpecies" />
      </div>
      <div>
        <label>
          Name:
        </label>
        <input type="text" v-model="newName" />
      </div>
      <div>
        <label>
          Date of Birth:
        </label>
        <input type="text" v-model="newDateOfBirth" />
      </div>
      <button>Add Animal</button>
    </form>
    <table>
      <tr>
        <th>Species</th>
        <th>Name</th>
        <th>Date of Birth</th>
      </tr>
      <tr v-for="(animal, index) in animals" :key="index">
        <td>{{ animal.species }}</td>
        <td>{{ animal.name }}</td>
        <td>{{ animal.dateOfBirth ? animal.dateOfBirth : "Unknown" }}</td>
        <button @click="removeFromList(index)">Remove</button>
        <button @click="moveToTop(index)">Move to top</button>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      newSpecies: "",
      newName: "",
      newDateOfBirth: "",
      animals: [
        { species: "bird", name: "Paja", dateOfBirth: null },
        { species: "dog", name: "Kala", dateOfBirth: new Date("2019") },
        { species: "dog", name: "Kica", dateOfBirth: new Date("2018") },
        { species: "cat", name: "Maza", dateOfBirth: new Date("2016") },
        { species: "horse", name: "Suza", dateOfBirth: new Date("2002") },
      ],
    };
  },
  methods: {
    removeFromList(index) {
      this.animals.splice(index, 1);
    },
    moveToTop(index) {
      const movingItem = this.animals.splice(index, 1);
      const movedItemToTop = this.animals.unshift(movingItem[0]);
      return movedItemToTop;
    },
    addAnimal() {
      this.animals.push({
        species: this.newSpecies,
        name: this.newName,
        dateOfBirth: this.newDateOfBirth,
      });
      this.newSpecies = "";
      this.newName = "";
      this.newDateOfBirth = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 10px;
}
a {
  color: #42b983;
}
table {
  margin: 30px auto;
}
table td {
  border: 1px solid grey;
}
</style>
