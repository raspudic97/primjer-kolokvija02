<template>
  <v-app id="inspire">
    <v-app-bar
      app
      color="white"
      flat
    >
      <v-container class="py-0 fill-height">
        <v-avatar
          class="mr-10"
          color="blue darken-1" 
          size="32"
        ></v-avatar>

        <v-btn
          v-for="link in links"
          :key="link.text"
          :to="link.path"
          text
        >
          {{ link.text }}
        </v-btn>

        <v-spacer></v-spacer>

        <v-responsive max-width="260">
          <v-text-field
            dense
            flat
            hide-details
            rounded
            solo-inverted
            placeholder="Unesite pojam.."
          ></v-text-field>
        </v-responsive>
      </v-container>
    </v-app-bar>

    <v-main class="grey lighten-3">

          <v-col>
            <v-sheet
              min-height="70vh"
              rounded="lg"
              style="padding:20px;"
            >
            
            <router-view></router-view>

            </v-sheet>
          </v-col>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      links: [
        {
          text: 'Naslovnica',
          path: '/'
        },
        {
          text: 'O nama',
          path: '/about'
        },
        {
          text: 'Profil',
          path: '/profile'
        },
        {
          text: 'Novosti',
          path: '/novosti'
        },
        {
          text: 'Kontakt',
          path: '/kontakt'
        },
      ],
      menuItems: [
        'Prva stavka',
        'Druga stavka',
        'Treća stavka',
        'Četvrta stavka' 
      ]
    }),
  }
</script>