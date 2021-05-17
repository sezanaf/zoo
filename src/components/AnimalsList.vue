<template>
  <div>
    <h1>
      Animals
    </h1>
    <ul>
      <li :key="index" v-for="(animal, index) in animals">
        {{ animal.species }}
        {{ animal.name }}
        {{ animal.birthday ? animal.birthday : "Unknown" }}
        <button @click="removeFromList(index)">Remove</button>
        <button @click="moveToTop(index)">Move to top</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      animals: [
        { species: "bird", name: "Paja", birthday: null },
        { species: "dog", name: "Kala", birthday: new Date("2019") },
        { species: "dog", name: "Kica", birthday: new Date("2018") },
        { species: "cat", name: "Maza", birthday: new Date("2016") },
        { species: "horse", name: "Suza", birthday: new Date("2002") },
      ],
    };
  },
  methods: {
    removeFromList(index) {
      this.animals.splice(index, 1);
    },
    moveToTop(index) {
      const movingItem = this.animals.splice(index, 1);
      const movingItemToTop = this.animals.unshift(movingItem[0]);
      return movingItemToTop;
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
</style>
