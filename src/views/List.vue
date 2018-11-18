<template>
  <div class="ui internally celled grid">
  <div class="row">
    <div class="three wide column">
      <img>
    </div>
    <div class="ten wide column">
      <div class="ui cards">
  <div v-for="book in state.books" class="card">
    <div class="content">
      <img class="right floated ui image" src="https://www.quadrante.com.br/skin/frontend/linkstore/default/images/logo.gif">
      <div class="description">
        {{ book.name }}
        <img class="right floated mini ui image" v-bind:src="book.image">
      </div>
      <div class="header">
        {{ book.price }}
      </div>
    </div>
    <div class="extra content">
      <div class="ui two buttons">
        <a target="_blank" v-bind:href="book.url" class="ui basic green button">Open</a>
      </div>
    </div>
  </div>
</div>
    </div>  
  </div>
</div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      state: {
        books: []
      }
    };
  },
  mounted: function() {
    const type = this.$route.query.type;
    const value = this.$route.query.value;
    const url = `http://localhost:5000/api/quadrante/book/Vida Eucaristica`;
    axios.get(url).then(r => {
      this.state.books = r.data;
      console.log(r.data);
    });
  }
};
</script>

