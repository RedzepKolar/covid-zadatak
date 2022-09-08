<template>
  <v-container grid-list-md>
  <v-card class="fix-cus" outlined>
    <v-list-item three-line>
      <v-list-item-content>
        <div class="text-overline mb-4">
          {{ cTitle }}
        </div>
        <v-list-item-title class="text-h4 mb-1">
          {{ cData }}
        </v-list-item-title>
      </v-list-item-content>
    </v-list-item>
  </v-card>
</v-container>
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

<style>
.fix-cus {
  text-align: center;
}
</style>