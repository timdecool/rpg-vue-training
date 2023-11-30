<script>
import charRow from './charRow.vue'

export default {
  name: 'charCreation',
  components: {
    charRow
  },
  data() {
    return {
      characters: [
      ],
      charClass: "Magicien",
      charName: "",
      statValue: 10

    }
  },
  computed: {
    mainStat: ({charClass}) => () => {
      let mainStat = "";
      if(charClass == "Magicien") {
        mainStat= "Intelligence"
      }
      if(charClass == "Guerrier") {
        mainStat = "Force"
      }
      if(charClass == "Archer") {
        mainStat = "Dextérité"
      }
      return mainStat;
    },
    className: ({charClass}) => () => {
      let className = '';
      if(charClass == "Magicien") {
        className = "Magicien";
      }
      if(charClass == "Guerrier") {
        className = "Guerrier"
      }
      if(charClass == "Archer") {
        className = "Archer"
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
          class: this.className(this.charClass),
          mainStat : this.mainStat(this.charClass),
          statValue : this.statValue
        })
      }
    },
    editChar(infos) {
      for(let i=0; i<this.characters.length; i++) {
        if(this.characters[i].id == infos.id) {
          this.characters[i].name = infos.name
          this.characters[i].class = infos.charClass
          this.characters[i].mainStat = infos.mainStat
          this.characters[i].statValue = infos.statValue
          console.log(infos.name)
        }
      }

    },
    deleteChar(id) {
      for(let i=0; i<this.characters.length; i++) {
        if(this.characters[i].id == id) {
          this.characters.splice(i,1);
        }
      }      
    },
    randomizeStat() {
      this.statValue = 3*(Math.ceil(Math.random()*6));
    },
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
      <select v-model="charClass" name="char-class" id="char-class">
        <option value="Magicien">Magicien</option>
        <option value="Guerrier">Guerrier</option>
        <option value="Archer">Archer</option>
      </select>
    </div>
    <div>
      <label for="main-stat">{{ mainStat(charClass) }}</label>
      <input type="number" name="main-stat" id="main-stat" max="20" min="0" v-model="statValue">
      <button @click="randomizeStat">Aléatoire</button>
    </div>
    <div id="form-button">
      <button @click="addChar">Ajouter le personnage</button>
    </div>
  </section>

  <p>{{ characters }}</p>

  <section>
    <table v-if="characters.length > 0">
      <tr>
        <th>N°</th>
        <th>Nom</th>
        <th>Classe </th>
        <th>Stat principale</th>
        <th>Valeur stat</th>
        <th>Actions</th>
      </tr>
      
      <tr v-for="character of characters">
        <char-row :character="character" @delete="deleteChar(character.id)" @edit="editChar"/>
      </tr>
    </table>
  </section>
</template>

<style scoped>
#char-creation {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  flex-wrap: wrap;
  gap: 10px;
  background-color: rgba(255, 123, 0, 0.096);
  border: 1px solid rgba(255, 123, 0, 0.199);
  padding: 30px;
}

#char-creation>div {
  display: flex;
  flex-direction:column;
}

#form-button {
  align-self: center;
}

input {
  margin-bottom: 5px;
}

h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

table {
  border-collapse: collapse;
  width: 100%;
  margin-top: 20px;
  
}
table, tr, th, td {
  border: 1px solid rgba(255, 123, 0, 0.199);
}

th {
  background-color: rgba(255, 123, 0, 0.096);

}

th, td {
  padding: 5px;
  text-align: center;
}

button {
  border: 0;
  border-radius: 3px;
  background-color:  rgb(143, 72, 5);
  padding: 7px 25px;
  color: lightgrey;
  cursor: pointer;
}

h3 {
  font-size: 1.2rem;
}
</style>
