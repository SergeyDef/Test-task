<template lang="pug">
  tr.table__line#table
    td.table__cell.cell__photo
      img(v-bind:src='user_data.avatarSrcFriend').table__photo
    td.table__cell
      span.table__text {{user_data.friendName}}
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
  mounted() {
    return{
      
    };
  },
  methods: {

  },
  data: function () {
    return {
      
    }
  },
}
</script>

<style lang="scss">

    .table__line{

    }
    .table__cell{
      width: 300px;
      height: auto;
      padding: 10px 0;
      background-color: #666666;
      border-left: 1px solid #fff;
    }
    .table__header{
      font-size: 22px;
      text-transform: uppercase;
    }
    .table__photo{
      width: 20%;
      height: 50px;
    }

</style>
