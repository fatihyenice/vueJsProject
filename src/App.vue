<template>
  <div class="container">

    <div v-if="step === 'loading'">
      Chargement...
    </div>

    <div v-else-if="step === 'error'">
      Impossible d'importer le fichier
    </div>

    <div v-else-if="step === 'ok'">
      <quizz :quizz="quiz" />
    </div>
  </div>
</template>


<script setup>
import { onMounted, ref } from 'vue';
import quizz from './components/quizz.vue';

const quiz = ref('');
const step = ref('loading');

onMounted(() => {

  fetch('/quizz.json')
  .then(r => {

      if(r.ok){
        step.value = "Fichier bien importé !";
        return r.json();
      }

      throw new Error("Fichier non importé, erreur !")
  })

  .then(data => {

    quiz.value = data
    step.value = "ok"

  })

  .catch((e) => {
    step.value = "error"
  })

});
</script>