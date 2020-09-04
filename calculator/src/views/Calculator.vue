<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <div class="text-center white--text">
          <h1>Calculator</h1>
        </div>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-data-table
          :headers="calculator_data.headers"
          :items="calculator_data.raw"
        >
        </v-data-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Chains from "../data/chains.json";
import ChainsHeaders from "../data/chains_headers.json";

export default {
  data: () => ({
    calculator_data: {
      headers: ChainsHeaders,
      raw: Chains,
    },
  }),
};
</script>

<style lang="sass" scoped></style>
