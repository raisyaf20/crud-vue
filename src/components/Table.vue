<template>
  <section class="mt-5">
    <div class="container">
      <h2 class="text-center color fw-semibold mb-3">List Product</h2>
      <div class="row justify-content-center">
        <div class="col-lg-10 col-md-10 col-sm-12">
          <table class="table">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Name</th>
                <th scope="col">Description</th>
                <th scope="col">Image</th>
                <th scope="col">Price</th>
                <th scope="col">Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(e, i) in item" :key="e.id">
                <td scope="row">{{ i + 1 }}</td>
                <td>{{ e.name }}</td>
                <td>{{ e.description }}</td>
                <td><img :src="e.image" alt="{e.name}" class="img-prod" /></td>
                <td>{{ e.price }}</td>
                <td>
                  <button
                    class="btn btn-primary"
                    @click="
                      hndlEdit(e.name, e.id, e.image, e.price, e.description)
                    "
                  >
                    Edit
                  </button>
                  <button
                    class="btn btn-danger"
                    @click="hndleDelete(e.name, e.id)"
                  >
                    Delete
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </section>

  <!-- Modal -->
  <div class="edit" :class="{ 'd-none': modal }">
    <h2>Edit Product</h2>
    <span>{{ nameEd }}</span>
    <form @submit.prevent="handleSubmit">
      <div class="mb-3">
        <label for="nm" class="form-label">Product Name</label>
        <input
          type="text"
          class="form-control"
          id="nm"
          v-bind:value="nameEd"
          name="nama"
        />
      </div>
      <div class="mb-3">
        <label for="desc" class="form-label">Description Product</label>
        <input
          type="text"
          class="form-control"
          id="desc"
          v-bind:value="desc"
          name="desc"
        />
      </div>
      <div class="mb-3">
        <label for="img" class="form-label">Image</label>
        <input
          type="file"
          name="img"
          id="img"
          class="form-control"
          @change="handleImageUpload"
        />
      </div>
      <div class="mb-3">
        <label for="pr" class="form-label">Price</label>
        <input
          type="number"
          id="pr"
          class="form-control"
          placeholder="100000 || wihtout comma"
          v-bind:value="price"
          name="pr"
        />
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>
    
    <script>
import axios from "axios";
export default {
  name: "TableComp",
  props: ["item"],
  data() {
    return {
      desc: "",
      price: "",
      image: null,
      imageUrl: "",
      modal: true,
      nameEd: "",
      imgCurrent: null,
      id: null,
    };
  },
  methods: {
    hndleDelete(nm, id) {
      if (window.confirm(`Are you sure Delete ${nm}`)) {
        axios.post(`http://localhost:7777/product/delete/${id}`).then((res) => {
          alert(res.data.msg);
          location.reload();
        });
      }
    },
    hndlEdit(nm, id, img, pr, desc) {
      this.id = id;
      this.modal = !this.modal;
      this.nameEd = nm;
      this.imgCurrent = img;
      this.desc = desc;
      this.price = pr;
    },
    handleSubmit(e) {
      e.preventDefault();
      const nm = e.target.elements.nama.value;
      const desc = e.target.elements.desc.value;
      const pr = e.target.elements.pr.value;

      let gmbr = this.image;
      let up = this.imgCurrent;

      if (gmbr) {
        this.imageUrl = URL.createObjectURL(gmbr);
      }

      if (this.imageUrl) {
        up = this.imageUrl;
      }
      axios
        .put(`http://localhost:7777/product/${this.id}`, {
          name: nm,
          description: desc,
          image: up,
          price: pr,
        })
        .then((res) => {
          alert(res.data.msg);
          e.target.reset();
          this.modal = true;
          location.reload();
        });
    },
    handleImageUpload(event) {
      this.image = event.target.files[0];
    },
  },
  mounted() {
    this.item;
  },
};
</script>
    
    <style>
.img-prod {
  width: 3.5rem;
}
table tr {
  vertical-align: middle;
  text-align: center;
}
.edit {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 29rem;
  background: #eaeaea;
  padding: 0.94rem;
  border-radius: 15px;
}
</style>