<template>

  <b-card :title="seed.subject" class="mb-2">
    <b-card-text>{{ seed.description }}</b-card-text>

    <b-button variant="outline-secondary" class="mr-2" @click="edit(seed)">
      Editar
    </b-button>
    <b-button variant="outline-danger" class="mr-2" @click="remove(seed)">
      Excluir
    </b-button>
  </b-card>
</template>

<script>
export default {
  name: 'ListItem',
  props: {
    seed: {
      type: Object,
      required: true,
      default: () => ({})
    },
  },
  methods: {
    remove(seed) {
      this.$emit('remove', seed);
    },
    edit(seed) {
      this.$emit('edit', seed);
    }
  }
};
</script>

<style>
</style>
