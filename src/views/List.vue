<template>
  <div class="ui celled grid">
    <div class="row">
      <header>
        <h1>Book Check Price</h1>
      </header>
    </div>
  <div class="row">
    <div class="sixteen wide column">
      <div class="ui cards">
        <div v-for="book in orderedBooks" class="card">
          <div class="content">
            <img class="small ui image">
            <div class="description">
              {{ book.name }}
              <img class="right floated tiny ui image" v-bind:src="book.image">
            </div>
            <div class="header">
              {{ book.price }}
            </div>
            <div class="ui two buttons">
              <a target="_blank" v-bind:href="book.url" class="ui basic green button">Open</a>
            </div>
          </div>
          <div class="extra content">
            
          </div>
        </div>
      </div>
    </div>  
  </div>
</div>
</template>

<script>
import axios from "axios";
import _ from "lodash";

export default {
  data: function() {
    return {
      state: {
        books: [
          // {
          //   image:
          //     "https://images.livrariasaraiva.com.br/imagemnet/imagem.aspx/?pro_id=7441739&qld=90&l=430&a=-1=1001508570",
          //   price: "55,90",
          //   url:
          //     "https://www.saraiva.com.br/os-miseraveis-edicao-especial-7441739.html",
          //   name: "Os Miseráveis",
          //   store: {
          //     image:
          //       "https://d1yjjnpx0p53s8.cloudfront.net/styles/logo-thumbnail/s3/042015/livraria_saraiva_0.png?itok=INHU88Jr",
          //     name: "Saraiva"
          //   }
          // }
        ]
      }
    };
  },
  computed: {
    type: function() {
      return this.$route.params.type;
    },
    value: function() {
      return this.$route.params.value;
    },
    orderedBooks: function() {
      return _.orderBy(this.state.books, ["price"]);
    }
  },
  mounted: function() {
    const stores = [
      "quadrante",
      "caritatem",
      "eRealizacoes",
      "livrariaFolha",
      "cultorDeLivros",
      "cancaoNova",
      "shalom",
      "sociedadeChestertonBrasil",
      "minhaBibliotecaCatolica",
      "santaCruz",
      "paulus",
      "familiaCrista",
      "ecclesiae",
      "deiaetiba",
      "bernardo",
      "seminarioFilosofia",
      "nandoMoura"
    ];
    stores.forEach(store => {
      const url = `http://localhost:5000/api/${store}/${this.type}/${
        this.value
      }`;
      axios
        .get(url)
        .then(r => (this.state.books = [...r.data, ...this.state.books]));
    });
  }
};
</script>

<style>
header {
  width: 100vw;
  height: 10vh;
  background-color: #ffdd77;
}
</style>


