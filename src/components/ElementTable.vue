<template lang="pug">
  tr(v-on:click="showWindow").table__line#table
    td.table__cell.cell__photo
      img(v-bind:src='user_data.avatarSrcFriend').table__photo
    td.table__cell
      span.table__text {{user_data.firstName}}
    td.table__cell
      span.table__text {{user_data.lastName}}
    td.table__cell
      span.table__text {{user_data.id}}
</template>

<script>
export default {
  name: "element-table",
  components: {

  },
  props: {
      user_data: {
        type: Object,
        default(){
          return {}
        }
      }
    },
  data: function () {
    return {
    }
  },
  mounted() {
    return{
      
    };
  },
  methods: {
    showWindow: function(){
      this.$emit('choose', this.user_data.id)
    }
  },
}
</script>

<style lang="scss">
    .table__line{
      background-color: #666666;
      cursor: pointer;
    }
    .table__line:hover {
      transition: background-color 1s, color 1s; 
      background-color: #ffdb8b;
      color: #333333;
      font-weight: 700;
    }
    .table__cell{
      width: 300px;
      height: auto;
      padding: 10px 0;
      font-size: 20px;
      border-left: 1px solid #fff;
    }

    .table__photo{
      width: 20%;
      height: 50px;
    }

</style>
