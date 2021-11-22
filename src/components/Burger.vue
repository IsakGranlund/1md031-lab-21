<template>
  <div >
    <span >
      <figure class="theme">
        <h1 v-bind:key=burger.name> {{ burger.name }}</h1>
        <img v-bind:src="burger.url" style="width: 330px; height: 350px">
        <ul>
          <li v-bind:key=burger.kCal> <span> {{burger.kCal}}</span>  Kalorier </li>
          <li v-if="burger.lactose"> Innehåller Laktos </li>
          <li v-else> Laktosfri </li>
          <li v-if="burger.gluten"> Innehåller Gluten </li>
          <li v-else> Glutenfri </li>
        </ul>
            <button type="button" v-on:click="addBurger">
              +
          </button>
        <button type="button" v-on:click="decease_burger">
              -
          </button>

    <p style="color: #ecc70f"> Antal  {{amountOrdered}}</p>
      </figure>

    </span>

  </div>
</template>

<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  },

  data: function () {
    return {
      amountOrdered: 0,
      orderedBurgers: "",
    }
  },
  methods: {
    addBurger: function () {
      this.amountOrdered += 1;
      this.$emit('orderedBurger', {
        name: this.burger.name,
            amount: this.amountOrdered
          }
      );
    },
    decease_burger() {
      if (this.amountOrdered > 0) {
        this.amountOrdered -= 1;
        this.$emit('orderedBurger', {
          name: this.burger.name,
          amount: this.amountOrdered
            }
        );
      }


    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>