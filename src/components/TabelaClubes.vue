<template>
  <div>
    <input type="text" class="form-control" v-model="busca" />
    <table class="table table-striped">
      <thead>
        <tr>
          <th>#</th>
          <th>Nome</th>
          <th v-for="(coluna, indice) in ordem.colunas">
            <a href="#" @click.prevent="ordenar(indice)">{{coluna | ucwords}}</a>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(time,indice) in timesFiltrados"
          :class="{'table-success': indice<6 }"
          :style="{'font-size': indice <6 ? '17px' : '15px'}"
        >
          <td>{{indice+1}}</td>
          <td>
            <clube :time="time"></clube>
          </td>
          <td>{{time.pontos}}</td>
          <td>{{time.gm}}</td>
          <td>{{time.gs}}</td>
          <td>{{time.saldo}}</td>
        </tr>
      </tbody>
    </table>
    <clubes-libertadores :times="timesOrdenados"></clubes-libertadores>
    <clubes-rebaixados :times="timesOrdenados"></clubes-rebaixados>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  inject: ["timesColecao"],
  data() {
    return {
      busca: "",
      ordem: {
        colunas: ["pontos", "gm", "gs", "saldo"],
        sort: ["desc", "desc", "asc", "desc"]
      },
      times: this.timesColecao
    };
  },
  computed: {
    timesFiltrados() {
      var self = this;
      return _.filter(this.timesOrdenados, function(time) {
        var busca = self.busca.toLowerCase();
        return time.nome.toLowerCase().indexOf(busca) >= 0;
      });
    },
    timesOrdenados() {
      return _.orderBy(this.times, this.ordem.colunas, this.ordem.sort);
    }
  },
  methods: {
    ordenar(indice) {
      this.$set(
        this.ordem.sort,
        indice,
        this.ordem.sort[indice] == "desc" ? "asc" : "desc"
      );
    }
  }
};
</script>