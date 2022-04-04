<template>
  <!-- Women Banner Section Begin -->
  <section class="women-banner spad">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12 mt-5" v-if="products.length > 0">
          <carousel
            class="product-slider"
            :items="3"
            :dots="false"
            :nav="false"
            :autoplay="true"
          >
            <div
              class="product-item"
              v-for="productItem in products"
              :key="productItem.id"
            >
              <div class="pi-pic">
                <img v-bind:src="productItem.galeries[0].photo" alt="" />
                <ul>
                  <li class="w-icon active">
                    <a href="#"><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view">
                    <router-link to="/product">Quick View</router-link>
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">{{ productItem.type }}</div>
                <a href="#">
                  <h5>{{ productItem.name }}</h5>
                </a>
                <div class="product-price">
                  {{ productItem.price }}
                  <span>$35.00</span>
                </div>
              </div>
            </div>
          </carousel>
        </div>
        <div class="col-lg-12" v-else>
          <p>Produk belum tersedia</p>
        </div>
      </div>
    </div>
  </section>
  <!-- Women Banner Section End -->
</template>

<script>
import carousel from "vue-owl-carousel";

export default {
  name: "BannerSection",
  components: {
    carousel,
  },
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    // Using Fetch
    fetch("http://127.0.0.1:8000/api/products")
      .then((result) => result.json())
      .then((result) => (this.products = result.data.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style scoped>
.product-item {
  margin-right: 25px;
}
</style>