<template>
  <ul class="list">
    <li></li>
    <template v-if="type === 'people'">
      <Item
        v-for="(character, index) in characters"
        :key="character.name + index"
        :item="character"
        @change="onChange(type, index)"
      />
    </template>
    <template v-else>
      <Item
        v-for="(planet, index) in planets"
        :key="planet.name + index"
        :item="planet"
        @change="onChange(type, index)"
      />
    </template>
  </ul>
</template>

<script>
import Item from "../components/Item.vue";

export default {
  name: "Items",
  components: {
    Item,
  },
  props: {
    type: String,
  },
  data() {
    return {
      characters: [],
      planets: [],
      characterNumbers: [],
      planetNumbers: [],
    };
  },
  created() {
    this.getData(this.type);
  },
  watch: {
    type() {
      if (this.type === "people" && this.characters.length === 0) {
        this.getData(this.type);
      } else if (this.type === "planets" && this.planets.length === 0) {
        this.getData(this.type);
      }
    },
  },
  methods: {
    getData(type) {
      if (type === "people") {
        this.random(this.characterNumbers, 83);
        this.characterNumbers.forEach((value, index) => {
          this.fetchData(type, value, index);
        });
      } else {
        this.random(this.planetNumbers, 83);
        this.planetNumbers.forEach((value, index) => {
          this.fetchData(type, value, index);
        });
      }
    },
    random(arr, max) {
      while (arr.length < 3) {
        const random = Math.floor(Math.random() * max) + 1;
        if (arr.indexOf(random) === -1) arr.push(random);
      }
    },
    async onChange(type, index) {
      if (type === "people") {
        let loop = true;
        while (loop) {
          const random = Math.floor(Math.random() * 83) + 1;
          if (this.characterNumbers.indexOf(random) === -1) {
            this.characterNumbers.splice(index, 1, random);
            loop = false;
          }
        }
        this.fetchData(type, this.characterNumbers[index], index);
      } else {
        let loop = true;
        while (loop) {
          const random = Math.floor(Math.random() * 83) + 1;
          if (this.planetNumbers.indexOf(random) === -1) {
            this.planetNumbers.splice(index, 1, random);
            loop = false;
          }
        }
        this.fetchData(type, this.planetNumbers[index], index);
      }
    },
    fetchData(type, id, index) {
      fetch(`https://swapi.dev/api/${type}/${id}/`, {
        method: "GET",
      })
        .then((res) => res.json())
        .then((data) => {
          if (type === "people") {
            const newCharacters = [...this.characters];
            newCharacters[index] = data;
            this.characters = newCharacters;
          } else {
            const newPlanets = [...this.planets];
            newPlanets[index] = data;
            this.planets = newPlanets;
          }
        });
    },
  },
};
</script>

<style scoped>
.list {
  list-style: none;
  margin: 0;
  padding: 0 10px;
  display: flex;
  gap: 10px;
}
</style>
