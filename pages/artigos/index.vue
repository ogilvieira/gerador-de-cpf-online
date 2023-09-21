<template>
  <v-container>
    <v-row>
      <v-breadcrumbs class="text-grey-darken-1" :items="breadcrumbsItems">
        <template v-slot:prepend>
          <v-icon size="small" icon="mdi-home"></v-icon>
        </template>
      </v-breadcrumbs>
    </v-row>
    <ContentList path="/artigos" v-slot="{ list }">
      <v-row v-for="article in list" :key="article._path">
        <v-col>
          <v-card
            color="primary"
            variant="outlined"
            :link="true"
            :to="article._path"
            :title="article.title"
            :text="article.description"
          ></v-card>
        </v-col>
      </v-row>
    </ContentList>
  </v-container>
</template>
<script lang="ts" setup>
  import { ref } from "vue";

  const breadcrumbsItems = ref([
    {
      title: 'Home',
      disabled: false,
      href: '/',
    },
    {
      title: 'Artigos',
      disabled: true,
      href: '/artigos',
    }
  ]);
</script>