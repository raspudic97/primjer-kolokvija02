<template>
  <div class="home">
    <v-text-field
      @input="apiInput"
      v-model="per_page"
      label="Per Page"
    ></v-text-field>

    <v-text-field @input="apiInput" v-model="page" label="Page"></v-text-field>

    <v-container class="grey lighten-5">
      <v-row class="mb-6" no-gutters>
        <v-col
          cols="3"
          v-for="rezultat in rezultati"
          :key="rezultat.id"
        >
          <v-card class="ma-4" width="400" outlined v-if="rezultat.year_established >= 2014">
            <v-list-item three-line>
              <v-list-item-content>
                <div class="text-overline mb-4">{{ rezultat.country }}</div>
                <v-list-item-title class="text-h5 mb-1">
                  {{ rezultat.name }}
                </v-list-item-title>
                <v-list-item-subtitle>
                  Trust Score {{ rezultat.trust_score }} || Year:
                  {{ rezultat.year_established }}</v-list-item-subtitle
                >
              </v-list-item-content>

              <v-list-item-avatar tile size="80" color="grey">
                <img :src="rezultat.image" :alt="rezultat.name" />
              </v-list-item-avatar>
            </v-list-item>

            <v-card-actions>
               <a :href="rezultat.url" target="_blank">
              <v-btn outlined rounded text>
               {{ rezultat.name }} web site
              </v-btn>
              </a>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      per_page: 20,
      page: 1,
      rezultati: [],
    };
  },
  methods: {
    apiInput: function () {
      const per_page_input = parseInt(this.per_page);
      const page_input = parseInt(this.page);

      if (!isNaN(per_page_input) && !isNaN(page_input)) {
        const URL = `https://api.coingecko.com/api/v3/exchanges?per_page=${this.per_page}&page=${this.page}`;

        this.axios.get(URL).then((response) => {
          this.rezultati = response.data;
        });
      } else {
        alert("Nije unesen broj");
        this.per_page = 20;
        this.page = 1;
      }
    },
  },
  created() {
    setInterval(() => {
      const URL = `https://api.coingecko.com/api/v3/exchanges?per_page=${this.per_page}&page=${this.page}`;

        this.axios.get(URL).then((response) => {
          this.rezultati = response.data;
        });

        console.log("Osvjezeno")
    }, 15000);
  }
};
</script>

<style scoped>
a {
  all: unset;
}
</style>
