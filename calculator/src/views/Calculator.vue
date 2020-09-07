<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <div class="text-center">
          <h1>Calculator</h1>
          <br />
          <!-- {{ temp }} -->
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
          :items="calculator_data.raw"
          :items-per-page="200"
          sort-by="final_building"
          :sort-desc="true"
          group-by="chain"
          show-group-by
          hide-default-footer
          dense
        >
          <template v-slot:[`item.number_needed`]="{ item }">
            <v-edit-dialog :return-value.sync="item.number_needed" large>
              <div class="font-italic">{{ item.number_needed }}</div>
              <template v-slot:input>
                <div class="mt-4">Number of final buildings needed.</div>
                <v-text-field
                  v-model="item.number_needed"
                  label="Edit"
                  single-line
                >
                </v-text-field>
              </template>
            </v-edit-dialog>
          </template>
          <template v-slot:[`item.electricity_supplied`]="{ item }">
            <v-simple-checkbox
              v-model="item.electricity_supplied"
              :disabled="!item.improved_by_electricity"
              :ripple="false"
            ></v-simple-checkbox>
          </template>
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
  computed: {},
  watch: {
    selected_chains: function(val) {
      // Update the table with the selected user chains.
      const new_data = [];
      for (let i = 0; i < val.length; i++) {
        for (let j = 0; j < this.initial_data.raw.length; j++) {
          if (val[i] === this.initial_data.raw[j].chain) {
            //  create initial table data
            new_data.push(this.initial_data.raw[j]);
            //  insert the defaults
          }
        }
      }
      for (let i = 0; i < new_data.length; i++) {
        if (new_data[i].final_building === true) {
          new_data[i].number_needed = 1;
        }
      }
      this.calculator_data.raw = new_data;
    },
    // calculator_data: {
    // deep: true,
    // handler(val) {
    //   // Set the initial number needed for final buildings
    //   for (let i = 0; i < val.raw.length; i++) {
    //     console.log(typeof val.raw[i].number_needed === "undefined");
    //     if (
    //       val.raw[i].final_building === true &&
    //       typeof val.raw[i].number_needed === "undefined"
    //     ) {
    //       val.raw[i].number_needed = 1;
    //       console.log("resetting to one");
    //     } else if (
    //       val.raw[i].final_building === false &&
    //       typeof val.raw[i].number_needed === "undefined"
    //     ) {
    //       val.raw[i].number_needed = "N/A";
    //     }
    //   }
    // },
    // },
  },
};
</script>

<style lang="sass" scoped></style>
