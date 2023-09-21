<template>
  <v-container>
    <v-row>
      <v-breadcrumbs class="text-grey-darken-1" :items="breadcrumbsItems">
        <template v-slot:prepend>
          <v-icon size="small" icon="mdi-home"></v-icon>
        </template>
      </v-breadcrumbs>
    </v-row>
    <v-row>
      <v-col>
        <article class="text-grey-darken-4 text-body-1">
          <ContentDoc>
            <template #not-found>
              <h2>Slug ({{ $route.params.slug }}) not found</h2>
            </template>
          </ContentDoc>
        </article>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" lg="6">
        <v-card color="primary" variant="outlined" v-if="prev" :to="prev._path" :text="prev.title">
        </v-card>
      </v-col>
      <v-col cols="12" lg="6">
        <v-card color="primary" variant="outlined" v-if="next" :to="next._path" :text="next.title">
        </v-card>
      </v-col>
    </v-row>

  </v-container>
</template>
<style>

article {
  line-height: 1.5em;
}

article p {
  margin: 1rem 0;
  text-align: justify;
  line-height: 1.5em;
}

article h1 {
  font-size: 2em;
  line-height: 1.3em;
  margin: 0 0 1.3em 0;
  color: rgb(var(--v-theme-primary));
  font-weight: 600;
}

article h2,
article h3,
article h4,
article h5,
article h6 {
  line-height: 1.3em;
  margin: 1.2em 0 0;
  font-weight: 600;
}

article strong {
  font-weight: 600;
}

article a[href^="#"] {
  text-decoration: none;
  color: inherit;
}
</style>
<script lang="ts" setup>
  import { ref } from "vue";
  import { useRoute } from "#vue-router";
  const route = useRoute();

  const breadcrumbsItems = ref([
    {
      title: 'Home',
      disabled: false,
      href: '/',
    },
    {
      title: 'Artigos',
      disabled: false,
      href: '/artigos',
    }
  ]);

  const [next, prev] = await queryContent('artigos').findSurround(route.fullPath);

</script>