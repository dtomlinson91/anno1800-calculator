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
          v-model="selected_chains"
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
          :items="get_calculator_data"
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
      headers: ChainsHeaders,
      raw: [],
    },
    selected_chains: [],
  }),
  methods: {
    get_production_chains: function() {
      const chains = [];
      for (let i = 0; i < this.initial_data.raw.length; i++) {
        chains.push(this.initial_data.raw[i].chain);
      }
      return [...new Set(chains)];
    },
  },
  computed: {
    get_calculator_data: function() {
      const new_data = [];
      for (let i = 0; i < this.selected_chains.length; i++) {
        for (let j = 0; j < this.initial_data.raw.length; j++) {
          if (this.selected_chains[i] === this.initial_data.raw[j].chain) {
            new_data.push(this.initial_data.raw[j]);
          }
        }
      }
      return new_data;
    },
  },
};
</script>

<style lang="sass" scoped></style>
