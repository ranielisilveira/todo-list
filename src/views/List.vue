<template>
  <div class="container mt-2">

    <Form ref="formRef" @update="getSeeds" />

    <div v-for="(seed, index) in seeds" :key="index">
      <ListItem :seed="seed" @remove="remove" @edit="edit" />
    </div>

    <Modal ref="modalRemove" @remove-seed="confirmRemoveSeed" />

  </div>
</template>

<script>
import Form from './Form.vue';
import ListItem from '../components/ListItem.vue';
import Modal from '../components/Modal.vue';
export default {
  name: "List",
  data() {
    return {
      seeds: [],
      seedSelected: [],

    };
  },
  mounted() {
    this.getSeeds();
  },
  methods: {
    getSeeds() {
      this.seeds = (localStorage.getItem("seeds")) ? JSON.parse(localStorage.getItem("seeds")) : [];
    },
    edit(seed) {
      this.$refs.formRef.setData(seed);
    },
    remove(seed) {
      this.seedSelected = seed;
      this.$refs.modalRemove.open(seed.subject);
    },
    confirmRemoveSeed() {
      this.seeds.splice(this.seeds.indexOf(this.seedSelected), 1);
      localStorage.setItem("seeds", JSON.stringify(this.seeds));
      this.$refs.modalRemove.hide();
    },
  },
  components: { Form, ListItem, Modal }
}
</script>
