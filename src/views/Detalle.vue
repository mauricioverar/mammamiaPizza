<template>
  <div class="detalle py-5 d-flex justify-content-center container">
    <div class="card mb-3"><!---->
      <div class="row g-0">
        <div
          class="col-md-5 img"
          :style="{ backgroundImage: `url(${pizza.img})` }"
        ></div><!--usando style v-bind-->
        <div class="col-md-7">
          <div class="card-body">
            <h3 class="card-title text-capitalize">{{ pizza.name }}</h3>
            <hr />
            <p class="card-text">
              {{ pizza.desc }}
            </p>
            <p class="card-text ">
              <b>Ingredientes:</b>
            </p>
            <ul><!--v-for para recorrer atributos de la pizza-->
              <li
                class="text-capitalize w-75"
                v-for="(ingrediente, i) in pizza.ingredients"
                :key="i"
              >
                &#127829; {{ ingrediente }}
              </li>
            </ul>

            <div class="d-flex justify-content-between">
              <h2 class=" text-dark">
                Precio: ${{ formatNumber(pizza.price) }}<!--hacer uso de la funcion externa creada en utils, pero registrarla como metodo en la instancia-->
              </h2><!--para poder tambn agregar pizza desde la vista de detalle-->
              <button class="btn btn-danger" @click="addToCart(pizza.id)"><!--CA agregar el evento clic, q ejecutara la action addToCart-->
                Añadir &#128722;
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";// para poder procesar los valores de state necesitamos getters CA agregamos mapActions
import utils from "@/utils/functions";
const { formatNumber } = utils;

export default {
  name: "Detalle",
  props: ["id"],
  computed: {
    ...mapGetters(["pizzaById"]),//declarando getters

    pizza() {//getter llamado pizza
      const { id } = this;
      return this.pizzaById(id);
    },
  },
  methods: { formatNumber, ...mapActions(["addToCart"]) },//registrando formatNumber (funcion global), como metodo dentro de la instancia
  //ca agregamos la action addToCart
};
</script>

<style scoped>
.img {
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}
</style>
