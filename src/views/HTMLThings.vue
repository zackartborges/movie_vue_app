<template>
  <div class="html-things">
    <h1>Hello World. I am big font.</h1>
    <h3>Welcome to the show page for some HTML.</h3>
    <div class="selection-html">
      <br />

      <label for="food">Whats your favorite?</label>
      <br />
      Popcorn -
      <input type="radio" name="food" id="popcorn" v-on:click="choosePopcorn" />
      <br />
      Rice -
      <input type="radio" name="food" id="rice" v-on:click="chooseRice" />
      <br />
      Chocolate -
      <input type="radio" name="food" id="chocolate" v-on:click="chooseChocolate" />
      <small v-if="chooseChocolate">WOW! Chocolate</small>
      <small v-if="choosePopcorn">Yum Popcorn</small>
      <small v-if="chooseRice">Rice!</small>
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
      choosePopcorn: false,
      chooseRice: false,
      chooseChocolate: false,
    };
  },
};
</script>
