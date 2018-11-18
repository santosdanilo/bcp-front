<template>
  <div class="ui four column centered grid">
  <div class="middle aligned row">
    <div class="column">
      <h1>Book Check Price</h1>
      <form class="ui form" v-on:submit.prevent="onSubmit">
        <div class="field">
          <input type="text" v-model="value" name="first-name" placeholder="Search by">
        </div>
        <div class="inline fields">
          <label for="fruit">Search by:</label>
          <div class="field">
            <div class="ui radio checkbox">
              <input type="radio" name="type" v-model="type" value="title" tabindex="0" class="hidden"  checked>
              <label>Title</label>
            </div>
          </div>
          <div class="field">
            <div class="ui radio checkbox">
              <input type="radio" name="type" v-model="type" value="author" tabindex="0" class="hidden">
              <label>Author</label>
            </div>
          </div>
          <div class="field">
            <div class="ui radio checkbox">
              <input type="radio" name="type" v-model="type" value="isbn" tabindex="0" class="hidden">
              <label>ISBN</label>
            </div>
          </div>
        </div>
        <button class="ui button" type="submit">Search</button>
      </form>
    </div>
  </div> 
</div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "home",
  data: () => {
    return {
      value: "",
      type: "book"
    };
  },
  methods: {
    onSubmit: function() {
      const params = {
        type: this.type,
        value: this.value
      };
      this.$router.push({ name: "search", params: params });
    }
  }
};
</script>
