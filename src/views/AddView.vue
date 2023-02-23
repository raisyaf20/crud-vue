<template>
  <section class="mt-5">
    <div class="container">
      <div class="row justify-content-center">
        <h2 class="color fw-bold text-center mb-3">Form Add Product</h2>
        <div class="col-lg-4 col-md-7 px-4">
          <form @submit.prevent="handleSubmit" class="card-add">
            <div class="mb-3">
              <label for="nm" class="form-label">Name Product</label>
              <input
                type="text"
                name="nama"
                class="form-control"
                id="nm"
                aria-describedby="emailHelp"
                v-model="nama"
              />
            </div>

            <div class="mb-3">
              <label for="desc" class="form-label">Description</label>
              <input
                type="text"
                name="desc"
                class="form-control"
                id="desc"
                v-model="desc"
              />
            </div>
            <div class="mb-3">
              <label for="pr" class="form-label">Price</label>
              <input
                type="text"
                name="price"
                class="form-control"
                id="pr"
                v-model="price"
              />
            </div>
            <div class="mb-3">
              <label for="img" class="form-label">Image</label>
              <input
                type="file"
                name="image"
                class="form-control"
                id="img"
                @change="handleImageUpload"
              />
            </div>
            <div v-if="imageUrl">
              <img :src="imageUrl" class="img-fluid" />
            </div>
            <button type="submit" class="btn btn-primary form-control">
              Submit
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      nama: "",
      desc: "",
      price: "",
      image: null,
      imageUrl: "",
    };
  },
  methods: {
    handleSubmit() {
      // mengambil value dari input field
      const name = this.nama;
      const desc = this.desc;
      const price = this.price;
      const image = this.image;

      // menampilkan image yang telah diupload
      if (image) {
        this.imageUrl = URL.createObjectURL(image);
      }

      axios
        .post("http://localhost:7777/product", {
          name: name,
          description: desc,
          image: this.imageUrl,
          price: price,
        })
        .then((respon) => {
          alert(respon.data.msg);
          window.location.assign("/");
        })
        .catch((err) => console.log(err));
    },
    handleImageUpload(event) {
      this.image = event.target.files[0];
    },
  },
};
</script>

<style>
.card-add {
  padding: 1.2rem;
  border-radius: 16px;
  box-shadow: -3px -3px 14px rgba(0, 0, 0, 0.25);
  border: 0.5px solid rgba(0, 0, 0, 0.25);
}
</style>