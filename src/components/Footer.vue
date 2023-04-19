<template>
  <div class="Footer-nav">
    Nombre de tâches : {{ listeTaches.length }}<br>
    tache en cours:{{nbTachesEnCours}}
    tache finis :{{nbTachesFinies}}<br>
  </div>
</template>

<script>
export default {
  name: 'Footer-nav',
  data() {
    return {
      nbTachesEnCours: 0,
      nbTachesFinies: 0,
    };
  },
  props: {
    listeTaches: {
      type: Array,
      default: () => [],
    },
  },
  watch: {
    listeTaches: {
      handler(listeTaches) {
        this.nbTachesEnCours = listeTaches.filter(tache => tache.statut === 'en cours').length;
        this.nbTachesFinies = listeTaches.filter(tache => tache.statut === 'finis').length;
      },
      immediate: true,
      deep: true,
    },
  },
};
</script>

<style scoped>
/* styles du composant */
</style>