<template>
  <h1>Home</h1>
  <label> <input type="checkbox" v-model="promptExit" /> Prompt to exit </label>
</template>

<script>
import { ref } from "vue";
import { onBeforeRouteLeave } from "vue-router";

export default {
  setup() {
    const promptExit = ref(true);

    onBeforeRouteLeave((to, from, next) => {
      if (promptExit.value) {
        window.Swal.fire({
          title: "You want to leave the page?",
          text: `There are unsaved changes that will be lost.`,
          icon: "warning",
          showCancelButton: true,
          buttonsStyling: false,
          cancelButtonColor: "#d33",
          confirmButtonColor: "#3085d6",
          confirmButtonText: "Yes, leave!",
          customClass: {
            confirmButton: "btn font-weight-bold btn-light-primary",
            cancelButton: "btn font-weight-bold btn-light-primary",
          },
          heightAuto: false,
        }).then((result) => {
          if (result.isConfirmed) {
            next();
          }
        });
      } else {
        next();
      }
    });

    return {
      promptExit,
    };
  },
};
</script>