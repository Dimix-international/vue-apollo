<template>
  <div v-if="loading">Loading..</div>
  <ul v-else>
    <li
        v-for="character in characters"
        :key="character.id"
    >
      {{character.name}}
    </li>
  </ul>
</template>

<script>

import {useQuery} from '@vue/apollo-composable';
import allCharacters from './graphql/allCharacters.query.gql';
import {computed} from "vue";

export default {
  name: 'App',
  setup() {
    const {result, loading} = useQuery(allCharacters); //сразу станет ref
    const characters = computed(() => result.value?.characters.results ?? []);

    return {
      characters,
      loading,
    }
  },
}
</script>

<style>

</style>
