<template>
  <div class="q-pa-lg bg-cinema text-white">
    <h1 class="text-center text-h4 text-primary q-mb-lg">🎬 Welcome to Movie Club</h1>

    <div class="row q-gutter-md items-center q-mb-md justify-center">
      <q-btn
        @click="changeOrder"
        :label="asc ? 'Sort by rating: Ascending' : 'Sort by rating: Descending'"
        color="primary"
        icon="sort"
        glossy
        rounded
        text-color="white"
      />
    </div>

    <div class="column q-gutter-md">
      <div
        v-for="movie in sortedMovies"
        :key="movie.id"
        class="q-pa-sm"
      >
        <q-card class="my-card bg-card text-white">
          <div class="row no-wrap">
            <q-img
              :src="movie.image"
              style="cursor: pointer; width: 150px;"
              class="rounded-borders"
            />
            <div class="q-pa-md col">
              <div class="text-h6 text-weight-bold text-primary">
                {{ movie.title }}
              </div>
              <div class="q-mt-xs">
                <q-badge
                  :color="getRatingColor(movie.rating)"
                  align="top"
                  class="q-mb-xs"
                  text-color="white"
                >
                  Rating: {{ movie.rating }} / 5
                </q-badge>
              </div>
              <div class="text-body2 text-grey-4">
                Duration: {{ movie.duration }} minutes
              </div>
              <div class="text-body2 text-grey-4">
                Categories: {{ movie.categories.join(', ') }}
              </div>
              <q-btn
                color="primary"
                icon="favorite"
                label="Add to Favorites"
                size="sm"
                class="q-mt-sm"
                glossy
                rounded
                text-color="white"
              />
            </div>
          </div>
        </q-card>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const asc = ref(false)

const movies = ref([
  {
    id: 1,
    title: "Skyfall",
    rating: 4.6,
    duration: 143,
    categories: ["Action", "Thriller", "Spy"],
    image: "https://xl.movieposterdb.com/12_11/2012/1074638/xl_1074638_3d858916.jpg"
  },
  {
    id: 2,
    title: "Casino Royale",
    rating: 4.5,
    duration: 144,
    categories: ["Action", "Thriller", "Spy"],
    image:  "https://image.film.at/images/cfs_1864w/5022675/uvigE215SzXdsEFPN0XRFR9RPiA.jpg"
  },
  {
    id: 3,
    title: "Spectre",
    rating: 4.0,
    duration: 148,
    categories: ["Action", "Mystery", "Spy"],
    image: "https://www.reellifewithjane.com/wp-content/uploads/2015/09/Spectre-Poster-1.jpg"
  },
  {
    id: 4,
    title: "No Time To Die",
    rating: 4.4,
    duration: 163,
    categories: ["Action", "Thriller", "Spy"],
    image: "https://image.tmdb.org/t/p/w500/iUgygt3fscRoKWCV1d0C7FbM9TP.jpg"
  },
  {
    id: 5,
    title: "Dreams of Tomorrow",
    rating: 4.8,
    duration: 122,
    categories: ["Fantasy", "Adventure", "Drama"],
    image: "https://m.media-amazon.com/images/M/MV5BNmRkY2MzYzItZDdjZC00MzQ4LWE3MzEtNmVmODhiODI2MjRkXkEyXkFqcGdeQXVyMTIxMDcwMTEz._V1_FMjpg_UX1000_.jpg"
  },
  {
    id: 6,
    title: "Echoes of Time",
    rating: 4.2,
    duration: 115,
    categories: ["Sci-Fi", "Mystery"],
    image: "https://images-na.ssl-images-amazon.com/images/I/81C1czVBf1L.jpg"
  }
])

const changeOrder = () => {
  asc.value = !asc.value
}

const sortedMovies = computed(() =>
  [...movies.value].sort((a, b) =>
    asc.value
      ? a.rating - b.rating
      : b.rating - a.rating
  )
)

const getRatingColor = (rating) => {
  if (rating >= 4.5) return 'green'
  if (rating >= 3.5) return 'blue'
  if (rating >= 2.5) return 'orange'
  return 'red'
}
</script>

<style scoped>
.bg-cinema {
  background-color: #1a1a1a;
}

.text-primary {
  color: #00bcd4 !important;
}

.bg-card {
  background-color: #2b2b2b;
  border-radius: 16px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.4);
}

.my-card:hover {
  transform: scale(1.01);
  transition: transform 0.2s ease-in-out;
}
</style>
