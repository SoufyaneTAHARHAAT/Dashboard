<template>
  <v-app>
    <v-app-bar 
      class="px-3"
      color="grey-darken-4" 
      flat 
      density="compact"
    >
      <v-spacer />
      <v-tabs 
        v-model="selectedTab" 
        centered 
        color="grey-darken-1"
      >
        <v-tab 
          v-for="link in links" 
          :key="link"
        >
          {{ link }}
        </v-tab>
      </v-tabs>
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <v-row>
          <v-col
            cols="12"
            sm="2"
          >
            <v-sheet />
          </v-col>
          <v-col
            cols="12"
            sm="8"
          >
            <v-sheet 
              v-if="selectedTab === 0"
              min-height="70vh" 
              rounded="lg" 
              class="pa-4"
            >
              Page 0
              <h2 class="mt-4">
                Apps List
              </h2>
              {{ groupData }}
            </v-sheet>
            <v-sheet v-else>
              Page 1
            </v-sheet>
          </v-col>
          <v-col
            cols="12"
            sm="2"
          />
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

  const selectedTab = ref(0)
  const links = ref(["Home", "About"])

// APIcall
  onMounted(async() => {
    fetchData()
  })
  const apiResponse = ref()
  const groupData = ref([])


  const fetchData = async () => {
    try {
      const response = await axios.get('https://www.anthony-cardinale.fr/_placeholder/monetization-api.json')
      apiResponse.value = response.data.data
      console.log(apiResponse.value)
    }
    catch (error: unknown) {
      console.error(error)
    }
  }

</script>
