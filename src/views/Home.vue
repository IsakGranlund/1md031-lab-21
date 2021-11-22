
<template >

  <header class="theme"> <!-- Ändrar tab namn -->
    <div>
      <img src=https://www.luxuryrestaurantawards.com/wp-content/uploads/sites/9/2020/12/Susona-Bodrum-LXR-Hotels-Resorts-Malva-Restaurant-scaled.jpg id="headerpic" >
      <div class="center"> <h1>Välkommen till BurgerOnline</h1></div>
    </div>
  </header>


  <main>
    <div  class="wrapper">
      <Burger clas v-for="burger in burgers"
              v-bind:burger="burger"
              v-bind:key="burger.name"
              v-on:orderedBurger="addToOrder($event)"
                />
    </div>



    <section class="theme" >
      <h1>Kundinformation</h1>
      <form>
        <p>
          <label for="firstname">Fullständigt namn</label><br>
          <input type="text" id="firstname" v-model="fn" required="required" placeholder="För- och efternam">
        </p>

        <p>
          <label for="email">Email-Adress</label><br>
          <input type="email" id="email" v-model="em" required="required" placeholder="E-mail adress">
        </p>
        <!--
        <p>
           <label for="adress">Adress</label><br>
           <input type="text" id="adress" v-model="adrs" placeholder="Adress">
         </p>-->

         <!-- <p>
           <label for="Husnummer">Husnummer</label><br>
           <input type="text" id="Husnummer" v-model="husnr" placeholder="Husnummer">
         </p> -->
        <p>
          <label for="betalning">Betalningssätt</label>
          <select id="betalning" v-model="rcp"><br>
            <option>Swish</option>
            <option>Bitcoin</option>
            <option>Bankkort</option>
            <option>Kontant</option>
          </select>
        </p>
        <p>
        Tryck vart du vill få leverans
        </p>
        <div id="container" >
          <div id="map"  v-on:click="map_location">
            <div v-bind:style="{left: this.location.x +'px',
                        top: this.location.y + 'px'}">
              T
            </div>
          </div>
        </div>

        <p>
          Kön
          <br>
          <input type="radio" id="Kille" v-model="gender" value="Kille" >
          <label for="Kille">Kille</label><br>

          <input type="radio" id="Tjej" v-model="gender" value="female">
          <label for="Tjej">Tjej</label><br>

          <input type="radio" id="Annat" v-model="gender" value="noanswer">
          <label for="Annat">Annat</label>
        </p>

        <textarea rows="7" columns="25" >

                        </textarea><br>
        <button v-on:click="sendOrder"  type="submit"  >

            Place your order!

        </button>

      </form>
    </section>
  </main>






  <footer class="theme"><!-- end notes -->
    <hr background="black">
    <p> &copy; 2018 Isak Lökiga Burgers
    </p>

  </footer>




</template>

<script>
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'
import menu from '/Users/isak/WebstormProjects/Labb1/1md031-lab-21/src/assets/menu.json'
const socket = io();



const Menu_Array= menu
export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
      fn :"",
      /* adrs:"",*/
      em:"",
    /*  husnr:"",*/
      gender:"",

      orderedBurgers: {},
      rcp:"Swish",
      burgers: Menu_Array,
      location: { x: 0,
                  y: 0
      }
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },

    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;
    },
    sendOrder: function () {
      console.log(this.location)
      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
            details: {
              gender: this.gender,
              em:this.em,
              rcp:this.rcp,
              fn:this.fn,
              x: this.location.x,
              y: this.location.y
            },
            orderItems: [this.orderedBurgers]


          }
      );

    },
    map_location: function (event){
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top
      };
       this.location={
         x: event.clientX - 10 - offset.x,
         y: event.clientY - 10 - offset.y
       }
    },
  }
}
</script>

<style>


#mainbackground{
  background-color: black;
}

.theme {
  overflow: auto;
  color: #ecc70f;
  text-transform: uppercase;
  background-color: black;
  border: 2px solid #ecc70f;
  border-radius: 30px;
  grid-template-columns: auto auto auto;
  padding: 20px;

}
#headerpic{
  width: 100%;
  height: 500px;
  border-radius: 50%;
  opacity: 0.95;
}
#container{
  height: 500px;
  width: 1000px;
  overflow:scroll;
}

.center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 18px;
}

.wrapper {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: black;
  border: 2px solid #ecc70f;
  border-radius: 50px;
  padding: 20px;

}

.center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 18px;
}




#button:hover {
  cursor: pointer;
  background-color: #ecc70f;
}

.button{
  padding-top: 10px;
  padding-bottom: 10px;
}
/*#map {
  width: 1920px;
  height: 1078px;
  background: url("../../public/img/polacks.jpg");
  background-repeat: no-repeat;
  cursor: crosshair; }*/
#map {
  position: relative;
  margin: 0;
  padding: 0;
  background: url(/img/polacks.jpg);
  background-repeat: no-repeat;
  width:1920px;
  height: 1078px;
  cursor: crosshair;

}
#map div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
}


</style>


