<template>
  <ion-page>
    <!-- Content -->
    <ion-content>
      <div class="container">
        <!-- Button -->
        <div class="button-container">
          <ion-button @click="getData()" class="custom-button ion-padding">
            Refresh
          </ion-button>
        </div>

        <!-- Table -->
        <ion-grid class="custom-grid">
          <!-- Table Rows -->
          <ion-row
            v-for="(crypto, index) in cryptoData"
            :key="crypto.id"
            class="table-row"
          >
            <ion-col class="table-col text-center">
              <p class="text-top">Rank</p>
              <p class="text-bottom">{{ index + 1 }}</p>
            </ion-col>
            <ion-col class="table-col">
              <p class="text-top">{{ crypto.name }}</p>
              <p class="text-bottom">{{ crypto.symbol }}</p>
            </ion-col>
            <ion-col class="table-col">
              <p class="text-top">USD</p>
              <p class="text-bottom">{{ crypto.price_usd }}</p>
            </ion-col>
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
  mounted() {
    this.getData();
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
  padding: 0;
}

/* Button */
.custom-button {
  color: white !important;
  font-size: 14pt;
}
.button-container {
  display: flex;
  justify-content: center;
}

/* Table */
.custom-grid {
  color: #000;
  overflow: hidden;
  display: inline;
}
.table-col {
  padding: 0px;
}
.table-col p {
  padding: 0px;
  margin: 5px;
}
.text-center {
  text-align: center;
}
.table-row {
  padding: 10px;
  background: #fff1c5;
  border: 1px solid #efc74e;
}
.text-top {
  font-size: 10pt;
}
.text-bottom {
  font-size: 22pt;
  font-weight: bold;
}
</style>
