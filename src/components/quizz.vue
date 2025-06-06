<template>
    <h3>{{ quizz.title }}</h3>
    <Progress :actuel="etape" :max="quizz.questions.length - 1" />
    <Question :question="questionActuelle.question" />

    <ul>
        <li v-for="(choice, index) in questionActuelle.choices" :for="index">
            {{ choice }}
        
            <label><input type="radio" :id="index" :value="choice" checked v-model="choixSelected" name="choix"></label>
        </li> 

        <button @click="teste" type="button">Valider ma réponse</button>
    </ul>
  </template>
  
  <script setup>
  import Progress from './Progress.vue';
  import Question from './Question.vue';
  import { computed, ref } from 'vue';
  
  const props = defineProps({
    quizz: Object
  });
  
  const etape = ref(0);
  const choixSelected = ref('');
  
  const questionActuelle = computed(() => props.quizz.questions[etape.value]);
  const reponse = computed(() => questionActuelle.value.correct_answer);

  const teste = () => {
    if(choixSelected.value == ""){
        alert("Veuillez faire un choix !");
    }else{
        if(choixSelected.value == reponse.value){
            alert('Bravo !!')
            etape.value += 1
        }else{
            alert("erreur")
        }
    }
  }
  </script>
  