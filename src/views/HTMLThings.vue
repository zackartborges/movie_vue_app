<template>
  <div class="html-things">
    <h1>Hello World. I am big font.</h1>
    <h3>Welcome to the show page for some HTML.</h3>
    <div class="selection-html">
      <br />

      <label for="food">Whats your favorite?</label>
      <br />
      Popcorn -
      <input v-model="food" type="radio" value="popcorn" id="popcorn" />
      <br />
      Rice -
      <input v-model="food" type="radio" value="rice" id="rice" />
      <br />
      Chocolate -
      <input v-model="food" type="radio" value="chocolate" id="chocolate" />
      <h3>Favorite food: {{ food }}</h3>
    </div>
  </div>
</template>
<style>
.selection-html {
  padding-top: 60px;
}
</style>
//
<script>
export default {
  data: function () {
    return {
      food: "WBb",
    };
  },
};
</script>
