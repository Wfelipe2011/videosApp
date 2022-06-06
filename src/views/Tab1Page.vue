<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>{{ title }}</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-toolbar>
        <ion-searchbar
          @input="inputChange"
          :value="search"
          placeholder="Buscar"
        ></ion-searchbar>
      </ion-toolbar>

      <ion-list>
        <ion-item :key="movie?.id" v-for="movie in movies">
          <ion-thumbnail slot="start">
            <img
              class="img-circle"
              :src="
                'https://image.tmdb.org/t/p/w220_and_h330_face' +
                movie?.poster_path
              "
            />
          </ion-thumbnail>
          <ion-label class="ellipsis">
            <h5>
              {{ movie?.title }}
            </h5>
            <div class="flex">
              <p class="ellipsis">{{ movie?.overview }}</p>
              <!-- <ion-button fill="outline" slot="end">Detalhes</ion-button> -->
            </div>
          </ion-label>
        </ion-item>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref, watch } from "vue";
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonThumbnail,
  IonLabel,
  IonList,
  IonItem,
  IonSearchbar,
} from "@ionic/vue";

interface Movie {
  id: number;
  original_title: string;
  overview: string;
  poster_path: string;
  release_date: string;
  title: string;
}

export default defineComponent({
  name: "TabProfile",
  components: {
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonPage,
    IonThumbnail,
    IonLabel,
    IonList,
    IonItem,
    IonSearchbar,
  },
  setup() {
    const title = "Filmes";
    const movies = ref<Movie[]>([]);
    const search = ref("");
    let timer: number | undefined = undefined;

    const inputChange = (e: any) => (search.value = e.target.value);

    watch(search, (value) => {
      clearTimeout(timer);
      timer = setTimeout(async () => await getByNameMovies(value), 800);
    });

    onMounted(async () => {
      await getAllMovies();
    });

    async function getAllMovies() {
      const response = await fetch(
        "https://api.themoviedb.org/3/movie/popular?api_key=2a960bb3d2f1e070ebb34875cea28802&language=pt-BR&page=1"
      );
      const data = await response.json();
      movies.value = data.results;
    }

    async function getByNameMovies(search: any) {
      if (search.length > 0) {
        const response = await fetch(
          `https://api.themoviedb.org/3/search/movie?api_key=2a960bb3d2f1e070ebb34875cea28802&language=pt-BR&query=${search}&page=1`
        );
        const data = await response.json();
        movies.value = data.results;
      } else {
        await getAllMovies();
      }
    }
    return { title, movies, search, inputChange };
  },
});
</script>
<style scoped>
.img-circle {
  border-radius: 100%;
}

.ellipsis {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  width: 18em;
}

.flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
