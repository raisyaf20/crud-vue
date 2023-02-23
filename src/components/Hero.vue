<template>
  <main class="mt-4">
    <div class="container">
      <div class="row justify-content-center align-items-center">
        <div class="col-md-5 ord">
          <h2 class="mb-2 color">CRUD VUE</h2>
          <p class="mb-3">
            Implement CRUD with backend REST API integration. which my mentor
            created while learning the data fetching API. GitHub 'fake-api' link
            in the button below.
          </p>
          <a
            href="https://github.com/priambudiLB/fake-api"
            class="github-link"
            target="_blank"
            >Github</a
          >
        </div>
        <div class="col-md-5 text-center">
          <img src="../assets/logo.png" alt="logo" class="img-fluid" />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "HeroComp",
};
</script>

<style>
.github-link {
  padding: 0.68rem 1.9rem;
  text-decoration: none;
  background: salmon;
  color: #232323;
  background: #42b983;
  border-radius: 30px;
}
.github-link:hover {
  background: #57ca96;
  color: #fff;
}

@media screen and (max-width: 750px) {
  .ord {
    order: 2;
  }
}
</style>