<template>
    <div class="todo-list">
    <h2>Ajouter une tâche</h2>
    <form @submit.prevent="ajouterTache">
      <label>
        Contenu de la tâche :
        <input type="text" v-model="nouvelleTache.contenu" />
      </label>
      <label>
        Temps estimé (en heures) :
        <input type="number" v-model="nouvelleTache.tempsEstime" />
      </label>
      <label>
        Statut :
        <select v-model="nouvelleTache.statut">
          <option value="en cours">En cours</option>
          <option value="fini">Fini</option>
        </select>
      </label>
      <button type="submit">Ajouter</button>
    </form>
    <h2>Liste des tâches</h2>
    <ul class="listeTaches">
      <li v-for="(tache, index) in listeTaches" :key="index" :class="{ 'en-cours': tache.statut === 'en cours', 'finis': tache.statut === 'finis' }">
        {{ tache.contenu }} ({{ tache.tempsEstime }} h) - {{ tache.statut }}
        <button @click="tacheSelectionne(index)">Modifier</button>
        <button @click="supprimerTache(index)">Supprimer</button>
        <div v-if="selectionTache  && index === selectionTache.index">
          <h2>Modifier la tâche "{{ selectionTache.contenu }}"</h2>
          <form @submit.prevent="updateTask(index)">
            <label for="content">Contenu :</label>
            <input type="text" id="content" v-model="selectionTache.contenu">
            <label for="time">Temps :</label>
            <input type="number" id="time" v-model="selectionTache.tempsEstime">
            <label for="status">Statut :</label>
            <select id="status" v-model="selectionTache.statut">
              <option value="en cours">En cours</option>
              <option value="finis">Finis</option>
            </select>
            <button type="submit">Mettre à jour</button>
          </form>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      nouvelleTache: {
        contenu: "",
        tempsEstime: null,
        statut: "en cours",
      },
      listeTaches: [],
      selectionTache: null
    };
  },
  methods: {
    ajouterTache() {
      if (
          this.nouvelleTache.contenu !== "" &&
          this.nouvelleTache.tempsEstime !== null
      ) {
        this.listeTaches.push(this.nouvelleTache);
        this.nouvelleTache = {
          contenu: "",
          tempsEstime: null,
          statut: "en cours",
        };
      }
    }, updateTask: function (index) {
      this.listeTaches[index].contenu = this.selectionTache.contenu;
      this.listeTaches[index].tempsEstime = this.selectionTache.tempsEstime;
      this.listeTaches[index].statut = this.selectionTache.statut;
      console.log(this.listeTaches[index]);
      this.selectionTache = null;
    },
    tacheSelectionne(index) {
      let tache=this.listeTaches[index]
      this.selectionTache = {
        index:index,
        contenu: tache.contenu,
        tempsEstime: tache.tempsEstime,
        statut: tache.statut
      };
      console.log(this.selectionTache);
    },
    supprimerTache(index) {
      this.listeTaches.splice(index, 1);
    },
  },
};
</script>
<style>
.en-cours {
  color: green;
}

.finis {
  color: red;
}
.listeTaches
{
  list-style: none;
}
</style>
