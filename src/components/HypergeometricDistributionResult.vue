<template>
  <v-container>
    <v-data-iterator :items="items" hide-default-footer>
      <template v-slot:default="props">
        <v-row>
          <v-col
            v-for="item in props.items"
            :key="'data-table-' + item.name"
            cols="12"
            sm="6"
            md="4"
            lg="3"
          >
            <v-card root>
              <v-card-title class="subheading font-weight-bold">
                {{ 'Case: x=' + item.name }}
              </v-card-title>

              <v-divider></v-divider>

              <v-list dense>
                <v-list-item
                  v-for="(data, key, index) in (({ name, ...o }) => o)(item)"
                  :key="'item-entry-' + index"
                >
                  <v-list-item-content v-if="key != 'name'" class="text-lg-right">{{ key + item.name }}</v-list-item-content>
                  <v-list-item-content v-if="key != 'name'" class="text-lg-right">
                    {{ numeral(data).format(precision) }}
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </v-card>
          </v-col>
        </v-row>
      </template>
    </v-data-iterator>
  </v-container>
</template>

<script>

import vuetify from "@/plugins/vuetify";

export default {
  name: "HypergeometricDistributionResult",
  vuetify,
  data: function () {
    return {
      numeral: require("numeral"),
      precision: "0.000%",
    };
  },
  props: {
      items: Array
  },
};
</script>