<template>
  <v-container>
    <v-card ref="form">
      <v-row>
        <v-spacer></v-spacer>
        <v-col>
          <v-text-field
            v-model="cardsInDeck"
            label="Cards in Deck"
            solo
            :rules="[
              () => !!cardsInDeck || 'This field is required',
              () => /^\d+$/.test(cardsInDeck) || 'Must be a number',
            ]"
          ></v-text-field>
        </v-col>
        <v-col>
          <v-text-field
            v-model="cardsWanted"
            label="Wanted card #"
            solo
            :rules="[
              () => !!cardsWanted || 'This field is required',
              () => /^\d+$/.test(cardsWanted) || 'Must be a number',
            ]"
          ></v-text-field>
        </v-col>
        <v-col>
          <v-text-field
            v-model="cardsToDraw"
            label="Cards to draw"
            solo
            :rules="[
              () => !!cardsToDraw || 'This field is required',
              () => /^\d+$/.test(cardsToDraw) || 'Must be a number',
            ]"
          ></v-text-field>
        </v-col>
        <v-spacer></v-spacer>
      </v-row>
      <v-divider></v-divider>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary" text @click="calculate"> Calculate </v-btn>
      </v-card-actions>
    </v-card>
    <HypergeometricDistributionResult v-if="results.items" v-bind:items="results.items"/>
  </v-container>
</template>

<script>
// import Vue from "vue";
import HypergeometricDistributionResult from "./HypergeometricDistributionResult";

var Hypergeometric = require("@stdlib/stats/base/dists/hypergeometric/ctor");
// const HyperGeoDisResultCtor = Vue.extend(HypergeometricDistributionResult);

export default {
  name: "Calculator",
  components: {
    HypergeometricDistributionResult
  },
  data: () => {
    return {
      cardsInDeck: null,
      cardsWanted: null,
      cardsToDraw: null,
      formHasErrors: false,
      results: {items: null},
    };
  },
  methods: {
    calculate: function () {
      this.formHasErrors = false;

      const N = parseInt(this.cardsInDeck);
      const K = parseInt(this.cardsWanted);
      const n = parseInt(this.cardsToDraw);

      var hypergeometric = Hypergeometric(N, K, n);
      console.log(hypergeometric);

      let items = [];

      for (let i = 0; i <= n; i++) {
        let item = {};

        const pmf = hypergeometric.pmf(i);
        const cdf = hypergeometric.cdf(i);

        item.name = i;
        item["="] = pmf;
        item[">"] = 1 - cdf;
        item[">="] = pmf + item[">"];
        item["<"] = cdf - pmf;
        item["<="] = cdf;

        items.push(item);
      }

      console.log(items);

        this.results.items = items;

    },
  },
};
</script>