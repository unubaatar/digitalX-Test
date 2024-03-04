<template>
  <div>
    <Header></Header>

    <Footer style="margin-top: 480px;"></Footer>
  </div>
</template>



<script type="module" lang="ts">

import Header from './components/layouts/header.vue';
import Footer from './components/layouts/footer.vue';

export default {
  name : "Home",
  components: {Header , Footer},
  props: {
    child: {
      type    : Object as any,
      required: true,
    },
    itemSort: { type: String },
    
  },
  data() {
    return {
      language: "",
    };
  },
  mounted() {
    console.log("test")
  }
};
</script>