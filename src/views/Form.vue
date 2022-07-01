<template>
  <div class="container mt-2">
    <b-form>
      <b-form-group label="Inserir Sementes" label-for="subject">
        <b-form-input id="subject" v-model="seed.subject" type="text" placeholder="Ex: TBIO AUDAZ" required
          autocomplete="off"></b-form-input>
      </b-form-group>

      <b-form-group label="Descrição" label-for="description">
        <b-form-textarea id="description" v-model="seed.description" type="text"
          placeholder="Ex: Cultivar de ciclo precoce e mais completa do mercado. Cultivar que apresenta tipo de planta e potencial produtivo similar ao seu pai, TBIO TORUK, uma excelente sanidade de folha (Similar a TBIO Sossego), com ótimo nível de resistência a mancha Foliar, Bacteriose e Mosaico do Trigo. Destaque a elevada resistência a Giberela e Brusone."
          required autocomplete="off"></b-form-textarea>
      </b-form-group>

      <b-button @click="resetForm"> Cancelar </b-button>
      <b-button type="submit" variant="outline-primary" @click="saveSeed"> {{ seed.id ? 'Atualizar' : 'Adicionar' }}
      </b-button>
    </b-form>
  </div>
</template>

<script>
import ToastMixin from "@/mixins/toastMixin.js";

export default {
  name: "Form",

  mixins: [ToastMixin],

  data() {
    return {
      seed: {
        id: null,
        subject: "",
        description: ""
      },
    }
  },

  methods: {
    setData(seed) {
      this.seed = seed
    },
    saveSeed() {
      if (this.seed.id) {
        let seeds = JSON.parse(localStorage.getItem("seeds"));

        seeds[seeds.indexOf(seeds.find(seed => seed.id == this.seed.id))] = this.seed;

        localStorage.setItem("seeds", JSON.stringify(seeds));
        this.showToast("success", "Sucesso!", "Semente atualizada com suceso");
        this.resetForm();
        return;
      }

      this.seed.id = Math.random().toString(36);
      let seeds = (localStorage.getItem("seeds")) ? JSON.parse(localStorage.getItem("seeds")) : [];
      seeds.push(this.seed);
      localStorage.setItem("seeds", JSON.stringify(seeds));
      this.showToast("success", "Sucesso!", "Semente criada com suceso");
      this.resetForm();
    },

    resetForm() {
      this.$emit('update')
      this.seed = {
        id: null,
        subject: "",
        description: ""
      }
    }
  }
}
</script>
