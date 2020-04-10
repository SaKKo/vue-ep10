<template lang="html">
  <div>
    <div>
      <v-text-field v-model="query" label="Search"> </v-text-field>
      <v-btn @click="handleSearchManga">Search</v-btn>
    </div>
    <v-divider class="mt-2 mb-2"></v-divider>
    <div class="d-flex flex-wrap">
      <v-card
        v-for="manga in results"
        :key="manga.mal_id"
        class="ma-2"
        max-width="344"
        outlined
        @click="handleMangaClick(manga)"
      >
        <v-list-item three-line>
          <v-list-item-content>
            <div class="overline mb-4">Publishing: {{ manga.publishing }}</div>
            <v-list-item-title class="headline mb-1">
              {{ manga.title }}</v-list-item-title
            >
            <v-list-item-subtitle>
              {{ manga.synopsis }}
            </v-list-item-subtitle>
          </v-list-item-content>

          <img
            :src="manga.image_url"
            alt=""
            :style="{ width: '80px', marginTop: '10px' }"
          />
        </v-list-item>
      </v-card>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      query: '',
      results: []
    }
  },
  methods: {
    handleSearchManga() {
      const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}&page=1`
      axios.get(url).then((res) => {
        console.log(res.data)
        this.results = res.data.results
      })
    },
    handleMangaClick(manga) {
      console.log('MANGA', manga)
      window.location = manga.url
    }
  }
}
</script>

<style lang="css" scoped></style>
