<template>
  <div>
    <button class="btn btn-primary" @click="criarNovoJogo">Novo Jogo</button>
    <placar-modal :time-casa="timeCasa" :time-fora="timeFora" ref="modal"></placar-modal>
  </div>
</template>
<script>
export default {
  data() {
    return {
      times: this.timesColecao,
      timeCasa: null,
      timeFora: null
    };
  },
  inject: ["timesColecao"],
  methods: {
    criarNovoJogo() {
      var indiceCasa = Math.floor(Math.random() * 20),
        indiceFora = Math.floor(Math.random() * 20);
      this.timeCasa = this.timesColecao[indiceCasa];
      this.timeFora = this.timesColecao[indiceFora];
      const { modal } = this.$refs;
      modal.showModal();
    }
  }
};
</script>