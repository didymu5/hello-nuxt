<template>
<div>
  <nav-bar />
  <hero-promo />
  <section class="container">
    <div>

      <h1 class="title">
        alo
      </h1>

      <button class="button is-medium" @click="snackbar">
            Launch snackbar (default)
        </button>
    </div>
  </section>
</div>

</template>

<script>
import NavBar from '~/components/NavBar.vue';
import HeroPromo from "~/components/HeroPromo.vue";
export default {
  components: {
    HeroPromo,
    NavBar
  },
  asyncData(context) {
    return { name: "hello" };
  },
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start();
      setTimeout(() => this.$nuxt.$loading.finish(), 500);
    });
  },
  methods: {
    snackbar() {
      this.$snackbar.open(
        `Default, positioned bottom-right with a green 'OK' button`
      );
    },
    warning() {
      this.$snackbar.open({
        message: "Yellow button and positioned top-left",
        type: "is-warning",
        position: "is-top",
        actionText: "Retry",
        queue: false,
        onAction: () => {
          this.$toast.open({
            message: "Action pressed",
            queue: false
          });
        }
      });
    },
    danger() {
      this.$snackbar.open({
        duration: 5000,
        message:
          "Snackbar with red action, positioned on bottom-left and a callback",
        type: "is-danger",
        position: "is-bottom-left",
        actionText: "Undo",
        onAction: () => {
          this.$toast.open({
            message: "Action pressed",
            queue: false
          });
        }
      });
    }
  }
};
</script>

<style>

</style>
