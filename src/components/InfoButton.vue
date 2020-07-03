<template lang="pug">
  .window
    .window__shut
      .shut
        span.shut__text x
      .window__wrapper
        .window__img
          img( src="https://i.pinimg.com/736x/af/f6/6e/aff66e7921d2394efdc5655614be6e43.jpg" )
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
  name: "info-button",
  components: {
  },
  data() {
    return {
     
    };
  },
  props: {
  },
  methods: {

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

    .window__img{
      width: 38%;
      margin: 3%;
      height: auto;

      img{
        width: 100%;
        height: auto;
      }
    }
    .window__info{
      width: 50%;
      margin: 3%;

      table{
        border: 2px solid #000;
        color: #fff;
        width: 100%;
        text-align: left;

        tr{
          background-color: #666666;
        }
        td{
          height: auto;
          padding: 10px 0;
        }
        span {
          margin-left: 5px;
          font-size: 18px;
        }
      }
    }
  }

</style>
