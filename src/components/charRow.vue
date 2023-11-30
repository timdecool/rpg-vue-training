<script>
export default {
    name:'charRow',
    data() {
        return {
            edit: false,
            id: this.character.id,
            name: this.character.name,
            charClass: this.character.class,
            statValue: this.character.statValue
        }
    },
    props: {
        character: {
            type: Object,
            require: true
        }
    },
    emits: ['delete', 'edit'],
    methods: {
        deleteRow() {
            this.$emit('delete')
        },
        editRow() {
            this.edit = !this.edit
            if(this.edit === false) {
                this.$emit('edit', {
                    id: this.id,
                    name: this.name,
                    charClass: this.charClass,
                    statValue: this.statValue,
                    mainStat: this.computeMainStat(this.charClass)
                })
            }          
        }
    },
    computed: {
        computeMainStat: ({charClass}) => () => {
            let mainStat = "yo";
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
        }
  },
}
</script>

<template>
        <td>
            {{ id }}
        </td>
        <td>
            <span v-if="!edit">{{ name }}</span>
            <input v-else type="text" id="name" v-model="name">
        </td>
        <td>
            <span v-if="!edit">{{ charClass }}</span>
            <select v-else id="name" v-model="charClass">
                <option value="Magicien">Magicien</option>
                <option value="Guerrier">Guerrier</option>
                <option value="Archer">Archer</option>
            </select>
        </td>
        <td>{{ computeMainStat(charClass) }}</td>
        <td>
            <span v-if="!edit">{{ statValue }}</span>
            <input v-else type="number" max="20" min="0" v-model="statValue">
        </td>
        <td>
            <button @click="editRow">
                <span v-if="!edit">Éditer</span>
                <span v-if="edit">Valider</span>
            </button>
            <button @click="deleteRow">Supprimer</button>
        </td>
</template>

<style>
td {
  padding: 5px;
  text-align: center;
}

td {
  border: 1px solid rgba(255, 123, 0, 0.199);
}

button {
  border: 0;
  border-radius: 3px;
  background-color:  rgb(143, 72, 5);
  padding: 7px 25px;
  color: lightgrey;
  cursor: pointer;
  margin-left: 5px;
}
</style>