<script>
export default {
  name: 'charCreation',
  props: {
  },
  data() {
    return {
      characters: [],
      mainStat: "mage",
      charName: "",
      statValue: 10

    }
  },
  computed: {
    className: ({mainStat}) => () => {
      let className = "";
      if(mainStat == "mage") {
        className= "Intelligence"
      }
      if(mainStat == "warrior") {
        className = "Force"
      }
      if(mainStat == "archer") {
        className = "Dextérité"
      }
      return className;
    }
  },
  methods: {
    addChar() {
      if(this.charName.length > 1) {
        this.characters.push({
          id: this.characters.length+1,
          name: this.charName,
          class: this.mainStat,
          mainStat : this.className(this.mainStat),
          statValue : this.statValue
        })
      }
    },
    deleteChar() {

    }

  }
}
</script>

<template>
  <section id="char-creation">
    <div>
      <label for="name">Nom du personnage</label>
      <input v-model="charName" type="text" name="name" id="name">
    </div>
    <div>
      <label for="char-class">Classe du personnage</label>
      <select v-model="mainStat" name="char-class" id="char-class">
        <option value="mage">Magicien</option>
        <option value="warrior">Guerrier</option>
        <option value="archer">Archer</option>
      </select>
    </div>
    <div>
      <label for="main-stat">{{ className(mainStat) }}</label>
      <input type="number" name="main-stat" id="main-stat" max="20" min="0" v-model="statValue">
      <button @click="">Aléatoire</button>
    </div>
    <div>
      <button @click="addChar">Ajouter le personnage</button>
    </div>
  </section>

  <section>
    <table>
      <tr>
        <th>N°</th>
        <th>Nom</th>
        <th>Classe </th>
        <th>Stat principale</th>
        <th>Valeur stat</th>
        <th>Actions</th>
      </tr>

      <tr v-for="character of characters">
        <th>{{ character.id }}</th>
        <th>{{ character.name }}</th>
        <th>{{ character.class }}</th>
        <th>{{ character.mainStat }}</th>
        <th>{{ character.statValue }}</th>
        <th><button>Supprimer</button></th>
      </tr>
    </table>
  </section>
</template>

<style scoped>
#char-creation {
  display: flex;
  gap: 10px;
}

h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
