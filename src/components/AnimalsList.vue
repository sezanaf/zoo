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
      <div>
        <label>Select sector: </label>
        <select v-model="newSector">
          <option v-for="(sector, index) in sectors" :key="index">
            {{ sector }}
          </option>
        </select>
      </div>
      <button>Add Animal</button>
    </form>
    <table>
      <tr>
        <th>Species</th>
        <th>Name</th>
        <th>Date of Birth</th>
        <th>Sector</th>
      </tr>
      <tr v-for="(animal, index) in animals" :key="index">
        <td>{{ animal.species }}</td>
        <td>{{ animal.name }}</td>
        <td>{{ animal.dateOfBirth ? animal.dateOfBirth : "Unknown" }}</td>
        <td>{{ animal.sector ? animal.sector : "Unknown" }}</td>
        <button @click="removeFromList(index)">Remove</button>
        <button @click="moveToTop(index)">Move to top</button>
      </tr>
    </table>

    <h2>Sector list</h2>
    <table>
      <tr>
        <th>Sector</th>
      </tr>
      <tr v-for="(sector, index) in sectors" :key="index">
        <td>{{ sector }}</td>
        <button @click="getAllAnimals(sector)">See all animals</button>
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
        { species: "maltezer", name: "Paja", dateOfBirth: null, sector: "Dog" },
        {
          species: "french bulldog",
          name: "Kala",
          dateOfBirth: new Date("2019"),
          sector: "Dog",
        },
        {
          species: "hasky",
          name: "Kica",
          dateOfBirth: new Date("2018"),
          sector: "Dog",
        },
        {
          species: "delfin",
          name: "Maza",
          dateOfBirth: new Date("2016"),
          sector: "Fish",
        },
        {
          species: "pony",
          name: "Suza",
          dateOfBirth: new Date("2002"),
          sector: "Horse",
        },
      ],
      sectors: ["Bird", "Dog", "Horse", "Fish"],
      sector: "",
      newSector: "",
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
        sector: this.newSector,
      });
      this.newSpecies = "";
      this.newName = "";
      this.newDateOfBirth = "";
    },
    getAllAnimals(sector) {
      const array = this.animals.filter((data) => data.sector === sector);
      const newArray = array.map((el) => {
        return ` (Species: ${el.species}, Name: ${el.name},  Date of Birth: ${el.dateOfBirth}, Sector: ${el.sector})`;
      });

      if (!newArray.length) {
        alert("There are no animals at this section");
      } else {
        alert(newArray);
      }
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
