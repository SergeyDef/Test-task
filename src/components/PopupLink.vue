<template lang="pug">
  .window( v-on:click="hideWindow" )
    .window__shut
      .shut( v-on:click="hideWindow" )
        span.shut__text x
      .window__wrapper
        span.window__information {{info_answer.answerInfo}}
   
</template>

<script>

export default {
  name: "popup-link",
  components: {
  },
  data() {
    return {
     
    };
  },
  props: {
    info_answer: {
      type:Object,
      default(){
        return {}
      }
    }
  },
  methods: {
    hideWindow: function (){
      this.$emit('hideInfo')
      },
  },
}
</script>

<style lang="scss" >
@import "~@/scss/fonts.scss";
@import "~@/scss/variables.scss";
@import "~@/scss/mixins.scss";

  .window{
    position: fixed;
    background-color: rgba(0,0,0,0.8);
    width: 100%;
    height: 100%;
    display: flex;
    margin: auto;

    .window__shut{
      margin: auto;
      display: flex;
      position: relative;
      width: 730px;
      height: 530px;
      border: 2px solid #000;
      background-color: #008000;
      border-radius: 10px;
    }

    .shut{
      cursor: pointer;
      position: absolute;
      background-color: #008000;
      width: 35px;
      height: 35px;
      top: -15px;
      right: 35px;
      display: flex;
      border-top: 2px solid #000;
      border-bottom: 2px solid #000;
      border-radius: 50px;
      padding-bottom: 3px;

      .shut__text{
        text-align: center;
        margin: auto;
        display: block;
        color: #fff;
        font-size: 28px;
        font-weight: 900;
        transition: 0.3s;
        text-align: center;
      }
    }

    .window__wrapper{
      width: 690px;
      height: 490px;
      margin: auto;
      background-color: #fff;
      border: 2px solid #000;
      display: flex;
    }
    .window__information{
      display: block;
      width: 100%;
      text-align: center;
      font-size: 35px;
      margin-top: 180px;
      font-weight: 900;
      color: #302c28; 
    }
  }

</style>
