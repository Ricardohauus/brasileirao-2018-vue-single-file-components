<template>
  <div class="container">
    <titulo></titulo>
    <div class="row">
      <div class="col-md-12">
        <novo-jogo :times="times"></novo-jogo>
      </div>
    </div>
    <br />
    <div class="row">
      <div class="col-md-12" v-show="visao === 'tabela'">
        <tabela-clubes :times="times"></tabela-clubes>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // time: new Time("América MG", "assets/america_mg_60x60.png"),
      times: [],
      visao: "tabela",
      timeCasa: null,
      timeFora: null
    };
  }
};
</script>
