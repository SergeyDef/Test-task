<template lang="pug">
  .disabled
    .disabled__img
      img( src='~@/assets/img/design_component/disabled_picture.gif')
       
    </template>
    
    <script>
    
    export default {
      name: "disabled-pages",
      components: {
      },
      data() {
        return {
    
        };
      },
      props: {
        user_info: {
          type:Object,
          default(){
            return {}
      }
    },
  },
  methods: {

  },
  mounted(){
    this.$nextTick(() => {
      
    });
  },
}
</script>

<style lang="scss" scoped>
@import "~@/scss/fonts.scss";
@import "~@/scss/variables.scss";
@import "~@/scss/mixins.scss";

.disabled{
  position: fixed;
  left: 0;
  top: 0;
  background-color: rgba(0,0,0,0.8);
  width: 100%;
  height: 100%;
  display: flex;
  margin: auto;

  .disabled__img{
    width: 50px;
    height: 50px;
    margin: auto;

    img{
      width: 100%;
      height: auto;
    }
  }
}
</style>
