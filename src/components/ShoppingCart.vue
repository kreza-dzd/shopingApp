<template>

        <PopupView :btn-text="totalCart" v-if="popupTriggers.buttonTrigger" :TogglePopup="() => TogglePopup('buttonTrigger')">

        </PopupView>
  <div class="container">
  <div class="row mt-2 justify-content-center">
      <div class="col-2" v-for="product in products" :key="product.id">
        <div class="card" style="width: 10rem;">
          <img :src="product.url" class="card-img-top"/>
          <div class="card-body">
            <h6 class="card-title">
              {{ product.name }} - € {{ product.price }}
            </h6>
            <button
            :disabled="product.cart"
              @click="addProduct(product)"
              href="#"
              class="btn  btn-block"
              :class="{
                'btn-primary': !product.cart,
                'btn-success': product.cart,
              }"
            >
              {{ !product.cart ? "Add" : "Added" }}
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="row mt-2">
      <table class="table  text-center">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Produkt</th>
            <th scope="col">Produktname</th>
            <th scope="col">Preis</th>
            <th scope="col">Menge</th>
            <th scope="col">Entfernen</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(product, index) in cart" :key="product.id">
            <th scope="row">{{ index + 1 }}</th>
            <th scope="row">
              <img :src="product.url" style="width: 4rem;" />
            </th>
            <td>{{ product.name }}</td>
            <td>
              {{ product.price }}€
            </td>
            <td>
              <button @click="decreaseQ(product)" class="btn btn-info btn-sm">
                -
              </button>
              {{ product.quantity }}
              <button
                @click="increaseQ(product)"
                class="btn btn-info btn-sm"
                size="sm"
              >
                +
              </button>
            </td>

            <td>
              <button @click="removeProduct(product)" class="btn btn-danger">
                X
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="row">
      <div class="col text-center">
        <h4>TOTAL: {{ totalCart }}€</h4>
        <button type="button" class="btn btn-primary" @click="() => TogglePopup('buttonTrigger')">Bezahlen</button>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, ref } from "vue";
import PopupView from './PopupView.vue';
export default {
  name: "ShoppingCart",
  setup() {


    const TogglePopup = (trigger) => {
    popupTriggers.value[trigger] = !popupTriggers.value[trigger]
   }

  const popupTriggers = ref({
    buttonTrigger: false,
    timedTrigger: false
});


    const cart = ref([]);
    const products = ref([
      {
        id: 1,
        name: "Shoe 1",
        price: 59,
        url:
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS8GlGnSZaUP27i0YqQe-mSIFTMRZwSM9sBrw&usqp=CAU",
        cart: false,
        quantity: 1,
      },
      {
        id: 2,
        name: "Shoe 2",
        price: 64,
        url:
          "https://theawesomer.com/photos/2022/03/kizik_shoes_t.jpg",
        cart: false,
        quantity: 1,
      },
      {
        id: 3,
        name: "Shoe 3",
        price: 39,
        url:
          "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTljnPR9k67rHLceRhsawZSqoQyOZEZWCAmkA&usqp=CAU",
        cart: false,
        quantity: 1,
      },


    ]);

    function addProduct(product) {
      cart.value.push(product);
      products.value.map((p) => {
        if (product.id == p.id) {
          p.cart = !p.cart;
        }
      });
    }
    function removeProduct(product) {
      cart.value = cart.value.filter((p) => p.id != product.id);
      products.value.map((p) => {
        if (product.id == p.id) {
          p.cart = !p.cart;
          p.quantity = 1;
        }
      });
    }
    function increaseQ(product) {
      products.value.map((p) => {
        if (product.id == p.id) {
          p.quantity += 1;
        }
      });
    }
    function decreaseQ(product) {
      products.value.map((p) => {
        if (product.id == p.id && p.quantity > 1) {
          p.quantity -= 1;
        }
      });
    }
    const totalCart = computed(() => {
      let t = 0;
      cart.value.forEach((e) => {
        t += e.quantity * e.price;
      });
      return t;
    });



    return {
      products,
      addProduct,
      increaseQ,
      removeProduct,
      decreaseQ,
      cart,
      totalCart,
      PopupView,
      popupTriggers,
      TogglePopup
    };

  },
  components: {
    PopupView
  }


};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.col-2 {
  z-index: 1;
background-color: #FFFFFF;
width:180px;
padding-top:80px;
height: 100%;
display: block;
margin: 0px;


}


@media screen and (max-width: 459px) {
  th {
    font-size: 12px;
  }

}


@media screen and (max-width: 400px) {
  th {
    font-size: 7px;
  }

}

</style>