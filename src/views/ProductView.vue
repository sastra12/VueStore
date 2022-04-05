<template>
  <div class="product">
    <HeaderBeetwen />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more">
              <router-link to="/"><i class="fa fa-home"></i>Home</router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="gambar_default" alt="" />
                </div>
                <div
                  class="product-thumbs"
                  v-if="
                    productDetails.galeries &&
                    productDetails.galeries.length > 1
                  "
                >
                  <carousel
                    class="product-thumbs-track ps-slider"
                    :dots="false"
                    :nav="false"
                  >
                    <div
                      v-for="picture in productDetails.galeries"
                      :key="picture.id"
                      class="pt"
                      @click="changeImage(picture.photo)"
                      :class="picture.photo == gambar_default ? 'active' : ''"
                    >
                      <img :src="picture.photo" alt="" />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details text-left">
                  <div class="pd-title">
                    <span>{{ productDetails.type }}</span>
                    <h3>{{ productDetails.name }}</h3>
                  </div>
                  <div class="pd-desc">
                    <p>
                      Lorem ipsum dolor sit amet consectetur adipisicing elit.
                      Corporis, error officia. Rem aperiam laborum voluptatum
                      vel, pariatur modi hic provident eum iure natus quos non a
                      sequi, id accusantium! Autem.
                    </p>
                    <p v-html="productDetails.description"></p>
                    <h4>${{ productDetails.price }}</h4>
                  </div>
                  <div class="quantity">
                    <!-- <router-link to="/cart" class="primary-btn pd-cart"
                      >Add To Cart</router-link -->
                    <a
                      @click="
                        saveCart(
                          productDetails.id,
                          productDetails.name,
                          productDetails.price,
                          productDetails.galeries[0].photo
                        )
                      "
                      href="#"
                      class="primary-btn pd-cart"
                      >Add To Cart</a
                    >
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->

    <RelatedProduct />

    <FooterSection />
  </div>
</template>

<script>
// @ is an alias to /src

import HeaderBeetwen from "@/components/HeaderBeetwen.vue";
import RelatedProduct from "@/components/RelatedProduct.vue";
import FooterSection from "@/components/FooterSection.vue";
import carousel from "vue-owl-carousel";
import axios from "axios";

export default {
  name: "ProductView",
  components: {
    HeaderBeetwen,
    RelatedProduct,
    FooterSection,
    carousel,
  },
  data() {
    return {
      gambar_default: "",
      productDetails: [],
      cartUser: [],
    };
  },

  methods: {
    changeImage(urlImage) {
      this.gambar_default = urlImage;
    },

    setDataPicture(data) {
      this.productDetails = data;
      this.gambar_default = data.galeries[0].photo;
    },

    saveCart(idProduct, productName, productPrice, productPhoto) {
      let productStored = {
        id: idProduct,
        name: productName,
        price: productPrice,
        photo: productPhoto,
      };

      this.cartUser.push(productStored);
      const parsed = JSON.stringify(this.cartUser);
      localStorage.setItem("cartUser", parsed);
    },
  },

  mounted() {
    if (localStorage.getItem("cartUser")) {
      try {
        this.cartUser = JSON.parse(localStorage.getItem("cartUser"));
      } catch (e) {
        localStorage.removeItem("cartUser");
      }
    }
    axios
      .get("http://127.0.0.1:8000/api/products/", {
        params: {
          slug: this.$route.params.slug,
        },
      })
      .then((result) => this.setDataPicture(result.data.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style scoped>
</style>
