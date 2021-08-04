<template>
  <div class="col-sm-6 col-md-4 mt-4">
    <div class="card border-success mb-3">
      <div class="card-header bg-info">
        <h3 class="card-title text-white">
          {{ stock.name }}
          <small class="fs-6"
            >(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small
          >
        </h3>
      </div>
      <div class="card-body text-success">
        <div>
          <div class="d-flex justify-content-center">
            <div class="col-md-6">
              <input
                type="number"
                class="form-control"
                placeholder="Quantity"
                v-model="quantity"
                :class="{
                  danger: insufficientQuantity,
                  normal: !insufficientQuantity,
                }"
              />
            </div>
            <div class="col-md-6 d-flex justify-content-end">
              <button
                class="btn btn-danger"
                @click="sellStock"
                :disabled="
                  insufficientQuantity ||
                  quantity <= 0 ||
                  !Number.isInteger(+quantity)
                "
              >
                {{ insufficientQuantity ? "Not enough" : "Sell" }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.danger {
  border-color: red;
  box-shadow: 0 0 0 0.2rem rgba(255, 0, 0, 0.418);
}
.normal {
  border-color: #28a745;
  box-shadow: 0 0 0 0.2rem rgba(40, 167, 69, 0.25);
}
</style>

<script>
import { mapActions } from "vuex";
export default {
  props: ["stock"],
  data() {
    return {
      quantity: 0,
    };
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    },
  },
  methods: {
    ...mapActions({
      placeSellOrder: "sellStock",
    }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      };
      this.placeSellOrder(order);
      this.quantity = 0;
    },
  },
};
</script>