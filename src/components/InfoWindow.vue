<template lang="pug">
  .window
    .window__img
    .window__info
       table
        tr
          td
            span registration date:
            span 
        tr
          td
            span surname:
            span 
        tr
          td
            span name:
            span 
        tr
          td
            span id:
            span 

</template>

<script>
export default {
  name: "modal-win",
  components: {

  },
  props: {
      user_data: {
      }
    },
  data: function () {
    return {
      info_determiner: true,
    }
  },
  mounted() {
    return{
      
    };
  },
  methods: {
  },
}
</script>

<style lang="scss">
  .window{
    left: 0;
    top: 0;
    background-color: #fff;
    width: 500px;
    height: 500px;
    display: flex;

    .window__img{
      width: 30%;
    }
  }

</style>
