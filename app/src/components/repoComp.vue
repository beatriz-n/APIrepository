<template>
  <v-form>
    <div class="text-center">
      <h1 class="erro" theme="dark" v-show="error === true">
        Erro, cheque os campos.
      </h1>
      <h4 class="texto">
        Para pesquisar repositorios informe apenas o usuario:
      </h4>
      <br />

      <v-container class="bg-surface-variant">
        <v-row class="mb-6" no-gutters>
          <v-col :cols="cols[0]">
          <v-responsive class="mx-auto" max-width="2000">
            <input
              placeholder="informe o usuario"
              class="texto texConf"
              v-model="usuario"
             
            />
          </v-responsive>
          </v-col>
          <v-col :cols="cols[0]">
          <v-btn variant="tonal" color="success" @click="envia" required>
            Enviar
          </v-btn>
          </v-col>
        </v-row>
      </v-container>

      <div class="lista"></div>
      <v-table theme="dark">
        <thead>
          <tr>
            <th class="text-left">ID</th>
            <th class="text-left">Nome</th>
            <th class="text-left">Linguagem</th>
            <th class="text-left">Proprietario</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in repo" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.language }}</td>
            <td>{{ item.owner.login }}</td>
          </tr>
        </tbody>
      </v-table>
      <div class="text-center">
        <v-pagination
          theme="dark"
          v-model="page"
          :length="3"
          :pageSize="8"
          color="success"
        ></v-pagination>
        <!-- <span v-if="(i, index) in new Array (10)" :key="index">
          <v-btn
        size="small"
        color="primary"
        @click="pageNum = index +1"
      >
      {{index +1}}
      </v-btn>
        </span> -->
      </div>
    </div>
  </v-form>
</template>
<script>
import axios from "axios";
export default {
  name: "repoComp",
  data() {
    return {
      page: 1,
      usuario: null,
      repo: null,
      error: false,
      //pageNum : 1,
    };
  },
  methods: {
    //botao enviar
    
    envia() {
      if (this.usuario == null) {
        this.error = true;
      } else {
        axios
          .get(`http://api.github.com/users/${this.usuario}/repos?page=${this.pageNum}&per_page=10`)
          .then((response) => {
            this.repo = response.data;
            console.log("id ", this.id);
          });
      }
    },
  },
  //mensagem de erro com tempo, para não poluir a tela
  watch: {
    error(val) {
      val &&
        setTimeout(() => {
          this.error = false;
        }, 2500);
    },
  },
  computed: {
      cols () {
        const { lg, sm } = this.$vuetify.display
        return lg ? [3, 9] : sm ? [9, 3] : [6, 6]
      },
    },
};
</script>
<style scoped>
.input {
  width: 50%;
}
.texto {
  color: aliceblue;
  padding-top: 1rem;
}
.texConf {
  width: 30%;
  padding: 1%;
  background-color: #1b242f;
}
.lista {
  padding-left: 10%;
}
.erro {
  color: rgb(255, 102, 102);
}
</style>