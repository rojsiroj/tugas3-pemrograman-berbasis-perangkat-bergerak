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
          <ion-row
            v-for="crypto in cryptoData"
            :key="crypto.id"
            class="table-row"
          >
            <ion-col>{{ crypto.name }}</ion-col>
            <ion-col>{{ crypto.symbol }}</ion-col>
            <ion-col>{{ crypto.price_usd }}</ion-col>
          </ion-row>
        </ion-grid>
      </div>
    </ion-content>
  </ion-page>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import axios, { AxiosResponse } from "axios";

// Definiskan interface struktur untuk cryptoData
interface CryptoData {
  id: string;
  name: string;
  symbol: string;
  price_usd: string;
}

// Definisikan interface untuk object response CryptoData
interface ResponseCryptoData {
  data: CryptoData[];
}

export default defineComponent({
  name: "HomePage",
  data() {
    return {
      cryptoData: [] as CryptoData[],
    };
  },
  methods: {
    async getData(): Promise<void> {
      try {
        // Fetch data dengan axios
        const response: AxiosResponse<ResponseCryptoData> = await axios.get(
          "https://api.coinlore.net/api/tickers/"
        );

        this.cryptoData = response.data.data;
      } catch (error) {
        console.error(error);
      }
    },
  },
});
</script>

<style scoped>
/* Container */
.container {
  padding: 10px 0px;
}

/* Button */
.custom-button {
  color: white !important;
}
.button-container {
  display: flex;
  justify-content: center;
  margin: 16px;
}

/* Table */
.custom-grid {
  border: 2px solid #000;
  color: #000;
  overflow: hidden;
}
.table-header {
  font-weight: bold;
  border-bottom: 2px solid #000;
  padding: 10px;
}
.table-row {
  padding: 10px;
}
</style>
