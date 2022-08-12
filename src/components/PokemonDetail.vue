<template>
  <div class="detail">
    <div class="detail-view" v-if="show">
      <div v-if="pokemon" class="image">
        <img
          :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.id}.png`"
          alt=""
        />
      </div>
      <div v-if="pokemon" class="data">
        <h2>{{ pokemon.name }}</h2>
        <div class="property">
          <div class="left">Base Experience</div>
          <div class="right">{{ pokemon.base_experience }} XP</div>
        </div>
        <div class="property">
          <div class="left">Height</div>
          <div class="right">{{ pokemon.height / 10 }} m</div>
        </div>
        <h3>Pokemon Types</h3>
        <div class="types">
          <div class="type" 
            v-for="(value, index) in pokemon.types"
            :key="'value'+index">
            {{ value.type.name }}
          </div>
        </div>
        <h3>Abilities</h3>
        <div class="abilities">
          <div class="ability" 
            v-for="(value, index) in pokemon.abilities"
            :key="'value'+index">
            {{ value.ability.name }}
          </div>
        </div>
      </div>
      <button class="close" @click="closeDetail">close</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: ["pokemonUrl"],
  data() {
    return {
      show: false,
      pokemon: {},
    };
  },
  methods: {
    closeDetail() {
      this.$emit("closeDetail");
    },
  },
  mounted() {
    axios.get(this.pokemonUrl).then((response) => {
      this.pokemon = response.data;
      this.show = true;
    });
  },
};
</script>

<style scoped>
.image {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: -60px;
  width: 120px;
  height: 120px;
  background-color: #333;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
.detail {
  display: flex;
  justify-content: center;
  align-items: flex start;
  flex-direction: column;
  position: fixed;
  top: 0;
  left: 0;
  padding: 10px 10px 10px;
  width: calc(100%);
  height: calc(100vh);
  background: rgba(0, 0, 0, 0);
}
.detail-view {
  align-self: center;
  display: flex;
  justify-content: 0;
  align-items: center;
  flex-direction: column;
  position: relative;
  width: 100%;
  max-width: 510px;
  padding: 50px 0 0;
  background-color: #fff;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
}

.close {
  outline: none;
  border: none;
  border-radius: 5px;
  background-color: #333;
  color: #efefef;
  padding: 10px 20px;
  margin-bottom: 20px;
  font-size: 1.2rem;
  cursor: pointer;
}
.property {
  width: 90%;
  max-width: 400px;
  border-bottom: 1px solid #ccc;
  margin-bottom: 10px;
}
.left {
  float: left;
}
.right {
  float: right;
}
.types, .abilities {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
  width: 90%;
  max-width: 400px;
}
.type, .ability {
  margin: 0 10px 10px 0;
  padding: 5px 10px;
  border-radius: 20px;
  color: #fff;
  font-size: 1rem;
  letter-spacing: 2px;
  text-transform: capitalize;
  word-wrap: none;
  word-break: keep-all;
}
.type { background-color: #0A2E50; }
.ability { background-color: #C73015; }
</style>