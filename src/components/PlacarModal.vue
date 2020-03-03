<template>
  <modal ref="modal">
    <h5 slot="header" class="modal-title">Novo Jogo</h5>

    <form slot="body" class="form-inline">
      <input type="number" class="form-control" v-model="golsCasa" />
      <clube :time="timeCasa" invertido="true" v-if="timeCasa"></clube>
      <span>X</span>
      <clube :time="timeFora" v-if="timeFora"></clube>
      <input type="number" class="form-control" v-model="golsFora" />
    </form>

    <div slot="footer">
      <button type="button" class="btn btn-primary" @click="fimJogo">Fim de Jogo</button>
    </div>
  </modal>
</template>

<script>
export default {
  data() {
    return {
      golsCasa: 0,
      golsFora: 0
    };
  },
  props: ["timeCasa", "timeFora"],
  methods: {
    showModal() {
      this.getModal().show();
    },
    closeModal() {
      this.getModal().close();
    },
    getModal() {
      return this.$refs.modal;
    },
    fimJogo() {
      var golsMarcados = parseInt(this.golsCasa);
      var golsSofridos = parseInt(this.golsFora);
      this.timeCasa.fimJogo(this.timeFora, golsMarcados, golsSofridos);
      this.closeModal();
      this.golsCasa = 0;
      this.golsFora = 0;
    }
  }
};
</script>