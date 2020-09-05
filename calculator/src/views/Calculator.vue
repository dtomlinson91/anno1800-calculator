<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <div class="text-center">
          <h1>Calculator</h1>
        </div>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-select
          :items="get_production_chains()"
          label="Select chains"
          chips
          multiple
          hint="Pick the production chains needed."
          persistent-hint
        ></v-select>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <v-data-table
          :headers="initial_data.headers"
          :items="initial_data.raw"
          :items-per-page="200"
          group-by="chain"
          show-group-by
          dense
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
    initial_data: {
      headers: ChainsHeaders,
      raw: Chains,
    },
    calculator_data: {
      headers: [],
      raw: [],
    },
  }),
  methods: {
    get_production_chains: function() {
      let chains = []
      for (let i = 0; i < this.initial_data.raw.length; i++) {
        chains.push(this.initial_data.raw[i].chain)
      }
      return [...new Set(chains)]
    }
  }
};
</script>

<style lang="sass" scoped></style>
