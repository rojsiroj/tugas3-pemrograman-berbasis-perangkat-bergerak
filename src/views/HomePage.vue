<template>
  <ion-page>
    <!-- Content -->
    <ion-content>
      <div class="container">
        <!-- Button -->
        <div class="button-container">
          <ion-button @click="getData()" class="custom-button">
            Get Data
          </ion-button>
        </div>

        <!-- Table -->
        <ion-grid class="custom-grid">
          <!-- Table Header -->
          <ion-row class="table-header">
            <ion-col>Name</ion-col>
            <ion-col>Symbol</ion-col>
            <ion-col>Harga USD</ion-col>
          </ion-row>

          <!-- Table Rows -->
          <ion-row class="table-row">
            <ion-col>Bitcoin</ion-col>
            <ion-col>BTC</ion-col>
            <ion-col>50,000</ion-col>
          </ion-row>
        </ion-grid>
      </div>
    </ion-content>
  </ion-page>
</template>
<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  methods: {
    async getData(): Promise<void> {},
  },
});
</script>

<style scoped>
.container {
  background: white;
  padding: 10px 0px;
}
.custom-button {
  color: white !important;
}
.custom-grid {
  border: 2px solid #000;
}
.button-container {
  display: flex;
  justify-content: center;
  margin: 16px;
}
</style>
