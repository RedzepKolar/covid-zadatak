<template>
  <v-card max-width="344" outlined>
    <v-list-item three-line>
      <v-list-item-content>
        <div class="text-overline mb-4">
          {{ cTitle }}
        </div>
        <v-list-item-title class="text-h5 mb-1">
          {{ cData }}
        </v-list-item-title>
      </v-list-item-content>
    </v-list-item>
  </v-card>
</template>

<script>
export default {
  name: "CustomCard",
  props: ['c-title', 'c-data'],
  data() {
    return {}
  }
};
</script>
