<template>
  <nav
    class="navbar navbar-expand-lg navbar-light"
    style="background-color: #9ec5fe"
  >
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand fs-2 fw-bold"
        >Stock Trader</router-link
      >
      <div class="collapse navbar-collapse">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <router-link
            class="nav-item fs-5"
            to="/portfolio"
            activeClass="active"
            tag="li"
            ><a class="nav-link">Portfolio</a></router-link
          >
          <router-link
            class="nav-item fs-5"
            to="/stocks"
            activeClass="active"
            tag="li"
            ><a class="nav-link">Stocks</a></router-link
          >
        </ul>

        <div class="d-flex">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item fs-5">
              <a class="nav-link" href="#" @click="endDay">End Day</a>
            </li>
            <li class="nav-item dropdown fs-5">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdown"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Save & Load
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                <li>
                  <a class="dropdown-item" href="#" @click="saveData"
                    >Save Data</a
                  >
                </li>
                <li>
                  <a class="dropdown-item" href="#" @click="loadData"
                    >Load Data</a
                  >
                </li>
              </ul>
            </li>
          </ul>
        </div>
        <div class="navbar-right navbar-text">
          <strong>Funds: {{ funds | currency }}</strong>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapActions } from "vuex";
export default {
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
  },
  methods: {
    ...mapActions({
      randomizeStocks: "randomizeStocks",
      fetchData: "loadData",
    }),
    endDay() {
      this.randomizeStocks();
    },
    saveData() {
      const data = {
        funds: this.$store.getters.funds,
        stockPortfolio: this.$store.getters.stockPortfolio,
        stocks: this.$store.getters.stocks,
      };
      this.$http.put("data.json", data);
    },
    loadData() {
      this.fetchData();
    },
  },
};
</script>
