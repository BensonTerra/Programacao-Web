<template>
  <v-container>
    <v-row>
      <v-col v-for="character in characters" :key="character.id" cols="4">
        <v-card class="mx-auto" max-width="1400">
          <v-img
            class="align-end text-white"
            height="200"
            :src="character.imageUrl"
            cover
          >
            <v-card-title>{{ character.name }}</v-card-title>
          </v-img>

          <v-card-subtitle class="pt-4"> 
            <p>Numero de filmes: {{ character.films.length }}</p>
            <p>Numero de curtas: {{ character.shortFilms.length }}</p>
            <p>Numero de programas: {{ character.tvShows.length }}</p>
            <p>Numero de jogos: {{ character.videoGames.length }}</p>
            <p>{{ character._id }}</p>
          </v-card-subtitle>
          

          <v-card-text>
            <div></div>
          </v-card-text>

          <v-card-actions class="d-flex align-center justify-center">
            <router-link 
            :to="{ name: 'character', params: { id: character._id }}">
              Ver mais
            </router-link>

            <p><a :href="wiki(character.name)" target="_blank">Ver na Disney Wiki</a></p>
          </v-card-actions>

        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import { useCharactersStore } from "@/stores/characters"
  import { RouterLink } from "vue-router";
  export default { 
    data() {
      return {
        characterStore: useCharactersStore(),
        character: null,
        wikiPage: null
      };
    },
    created () {
      try {
        this.characterStore.fetchCharacters();
      } catch (error) 
      {
        throw error;
      }
    },
    computed: {
      characters() {
        return this.characterStore.getCharacters;
      }
    },
    methods: {
      wiki(name) {
        let wikiUrl = "https://disney.fandom.com/wiki/" + name;
        return wikiUrl
      }
    },
  }
</script>

