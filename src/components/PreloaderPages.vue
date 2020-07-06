<template lang="pug">
  .window( v-on:click="hideWindow" )
    transition( name="window-info" )
      .window__shut( v-if="windowShut" )
        .shut( v-on:click="hideWindow" )
          span.shut__text x
        .window__wrapper
          .windom__user-info( v-if="windomUserInfo")
            h1.window__title Information about the user {{user_info.firstName + ' ' + user_info.lastName}}
            .window__user
              .window__img
                img( v-bind:src="user_info.avatarSrcFriend" )
              .window__info
                table
                  tr
                    td
                      span id: {{user_info.id}}
                      span 
                  tr
                    td
                      span name: {{user_info.firstName}}
                      span 
                  tr
                    td
                      span surname: {{user_info.lastName}}
                      span 
                  tr
                    td
                      span registration date: {{user_info.registrationDate}}
                      span 
          span(v-if="notification").window__information {{user_info.answerInfo}}
   
</template>

<script>

export default {
  name: "info-message",
  components: {
  },
  data() {
    return {
      windowShut: false,
      notification: false,
      windomUserInfo: false,

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
    hideWindow: function (){
      this.$emit('hide')
      },
  },
  mounted(){
    this.$nextTick(() => {
      this.windowShut = true
      this.user_info.sensor ? this.notification = true : this.windomUserInfo = true
      console.log(this.user_info.sensor)
    });
  },
}
</script>

<style lang="scss" scoped>
@import "~@/scss/fonts.scss";
@import "~@/scss/variables.scss";
@import "~@/scss/mixins.scss";

  .window{
    position: fixed;
    left: 0;
    top: 0;
    background-color: rgba(0,0,0,0.8);
    width: 100%;
    height: 100%;
    display: flex;
    margin: auto;

    .window-info-enter-active {
      animation: window-info-in 1.9s;
    }
    .window-info-leave-active {
      animation: window-info-in 1.9s reverse;
    }
    @keyframes window-info-in {
      0% {
        transform: scale(0);
      }
      50% {
        transform: scale(1.2);
      }
      100% {
        transform: scale(1);
      }
    }

    &__shut{
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

      &__text{
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

    &__wrapper{
      width: 690px;
      height: 490px;
      margin: auto;
      background-color: #fff;
      border: 2px solid #000;
      display: flex;
    }

    &__user-info{
      width: 100%;
      height: auto;
      display: flex;
      flex-direction: column;
    }

    .window__user{
      width: 100%;
      height: auto;
      display: flex;
    }
    .window__title{
      color: #333333;
      font-size: 25px;
      width: 80%;
      margin: auto;
      padding: 10px 0; 
    }

    &__img{
      width: 38%;
      margin: 3%;
      height: auto;

      img{
        width: 100%;
        height: auto;
      }
    }

    &__info{
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
    &__information{
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
