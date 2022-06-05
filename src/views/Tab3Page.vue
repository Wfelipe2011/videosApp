<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Sobre</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <div class="card">
        <img
          class="profile"
          src="https://avatars.githubusercontent.com/u/60045911?v=4"
          alt="Wilson"
        />
        <div class="card-content">
          <h1>Wilson Felipe</h1>
          <p>Desenvolvedor FullStack na Tegra</p>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";

export default defineComponent({
  name: "Tab3Page",
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
});
</script>
<style scoped>
.profile {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin: 0 auto;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 15px;
  margin: 10px;
}

.card-content {
  padding: 15px;
}
</style>
