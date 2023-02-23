<template>
  <div>
    <hero-comp />
    <table-comp :item="product" />
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
import HeroComp from "@/components/Hero.vue";
import TableComp from "@/components/Table.vue";

export default {
  name: "HomeView",
  components: {
    HeroComp,
    TableComp,
  },
  data() {
    return {
      product: null,
    };
  },
  mounted() {
    axios
      .get(`http://localhost:7777/product`)
      .then((res) => {
        this.product = res.data.data;
      })
      .catch((err) => alert(err.message));
  },
};
</script>
