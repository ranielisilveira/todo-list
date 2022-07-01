<template>
  <b-modal ref="modalRemove" hide-footer title="Exclusão de semente">
      <div class="d-block text-center">
        Deseja realmente excluir essa semente? {{ subject }}
      </div>
      <div class="mt-3 d-flex justify-content-end">
        <b-button variant="outline-secondary" class="mr-2" @click="hide"> Cancelar </b-button>
        <b-button variant="outline-danger" class="mr-2" @click="confirmRemoveSeed"> Excluir </b-button>
      </div> 
    </b-modal>
</template>

<script>
export default {
    name: "Modal",
    data() {
        return {
            subject: null
        };
    },
    methods: {
        open(subject) {
            this.subject = subject;
            this.$refs.modalRemove.show();
        },
        hide() {
            this.$refs.modalRemove.hide();
        },
        confirmRemoveSeed() {
            this.$emit('remove-seed');
        },
    }
}
</script>

<style>

</style>