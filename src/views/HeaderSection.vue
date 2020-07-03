<template lang="pug">
  .search
    h1.search__title {{ title }}
    button( v-on:click="getUsers" ).search__button request a list
    .search__form.form
      input.form__input#search
      button( v-on:click="searchUser" ).form__button search
      //select.form__method
        //option( value="1").form__method__item by name
        //option( value="2").form__method__item by id
    .search__users__list.table
      table
        tr
          td.table__cell
            span.table__header photo
          td.table__cell
            span.table__header name
          td.table__cell
            span.table__header surname
          td.table__cell
            span.table__header id
        element-table( 
          v-for="user in users"
          :key="user.id"
          v-bind:user_data="user"
         )
    info-button( v-if="infoIndicator" )
</template>

<script>
import InfoWindow from '@/components/InfoWindow';
import ElementTable from '@/components/ElementTable';
import InfoButton from '@/components/InfoButton';
import * as axios from 'axios';

export default {
  name: "search-users",
  components: {
    ElementTable,
    InfoWindow,
    InfoButton,
  },
  data() {
    return {
      title: 'find and sort users',
      users: [
        {
          id:1,
          firstName:"Марина",
          lastName:"Шипилова",
          avatarSrcFriend:"https://avatars.mds.yandex.net/get-pdb/1936494/b54ac088-fa39-4f4f-b8dd-1d387da466ae/s1200",
          registrationDate:"08.12.2014",
        },
        {
          id:2, 
          firstName:"Валерия",
          lastName:"Воротынцева", 
          avatarSrcFriend:"https://yt3.ggpht.com/a/AATXAJyeElqaUFj1Orn19o0Ux-EHBnPkx1sqqtaK8g=s900-c-k-c0xffffffff-no-rj-mo",
          registrationDate:"01.03.2016",
        },
        {
          id:3,
          firstName:"Lenka",
          lastName:"Drozdowa", 
          avatarSrcFriend:"https://yt3.ggpht.com/a/AGF-l78G1OYVfx10MRsHr3tzTjQ_FFMM6nt_cjiZzQ=s900-c-k-c0xffffffff-no-rj-mo",
          registrationDate:"09.07.2020",
        },
        {
          id:4, 
          firstName:"Алексей",
          lastName:"Башаров", 
          avatarSrcFriend:"https://img3.badfon.ru/wallpaper/big/3/2d/devushka-lico-elf-vzglyad-7450.jpg",
          registrationDate:"04.10.2019",
        },
        {
          id:5,
          firstName:"Катя",
          lastName:"Лапина",
          avatarSrcFriend:"https://i.pinimg.com/originals/8a/ec/c4/8aecc4b99cf3f2cf1ddd0052f934a527.jpg",
          registrationDate:"08.06.2015",
        },
        {
          id:6, 
          firstName:"Anna",
          lastName:"Tobulina", 
          avatarSrcFriend:"https://i.pinimg.com/originals/45/34/8c/45348c6e37956ee991a3ebd845e4d762.jpg",
          registrationDate:"10.01.2020",
        },
        {
          id:7, 
          firstName:"Пётр",
          lastName:"Роднов", 
          avatarSrcFriend:"https://i.pinimg.com/736x/99/1b/91/991b9187e4b6cbf0d0e2a170e04b6ceb.jpg",
          registrationDate:"15.04.2018",
        },
        {
          id:8, 
          firstName:"Елена",
          lastName:"Уткина", 
          avatarSrcFriend:"https://pbs.twimg.com/media/Drx3N9eU8AEXgjW.jpg",
          registrationDate:"27.09.2016",
        },
        {
          id:9, 
          firstName:"Тытьяна",
          lastName:"Нагиева", 
          avatarSrcFriend:"https://i.ytimg.com/vi/iAU8yKY9tAY/maxresdefault.jpg",
          registrationDate:"07.12.2015",
        },
        {
          id:10, 
          firstName:"Димон",
          lastName:"Антонов", 
          avatarSrcFriend:"https://trikky.ru/wp-content/blogs.dir/1/files/2018/07/23/c8a00eb61059d7e0507050742671f5a0.jpg",
          registrationDate:"11.10.2014",
        },
        {
          id:11, 
          firstName:"Нина",
          lastName:"Лунеева", 
          avatarSrcFriend:"https://i.pinimg.com/originals/bc/2d/42/bc2d4235943b77a438d330b6d4d54048.jpg",
          registrationDate:"11.12.2016",
        },
      ],
      info: null,
      infoIndicator: false,
    };
  },
  mounted() {
    axios
    .get('https://raw.githubusercontent.com/SergeyDef/nitrenJSON-/master/friends_profile.json')
    .then(response => (this.info = response));
  },
  methods: {
    getUsers: function () {
      console.log(this.info)
    },
    searchUser: function(){
      let input = document.getElementById('search');
      
      let results = this.users.filter(function(item){
        
        return item.id === +input.value ||
        item.firstName.toLowerCase() === input.value.toLowerCase() || 
        item.lastName.toLowerCase() === input.value.toLowerCase();
      });

      console.log(results);
      this.users = results
      console.log(input.value);
    },
  }
}

</script>
<style lang="scss" >
@import "~@/scss/fonts.scss";
@import "~@/scss/variables.scss";
@import "~@/scss/mixins.scss";

html{
  height: 100%;
  background-color: #333333;
}
body{
  height: 100%;
}
#app{
  height: 100%;
}
.search {
  width: 100%;
  min-height: 100%;
  margin: 0 auto;
  color: #fff;
  position: relative;
  background-color: #333333;

  .search__title{
    text-transform: uppercase;
    padding: 30px 0;
  }

  .search__button{
    position: absolute;
    top: 30px;
    left: 50px;
    padding: 10px 10px;
    color: #fff;
    text-transform: uppercase;
    background-color: #24baef;
    border-radius: .35714rem;
    font-weight: 600;
    border-color: #24baef;
  }

  .search__form{
    width: 100%;
    height: auto;
  }

  .form{

    .form__input{
      width: 550px;
      height: 35px;
      border-color: #24baef;
      border-radius: .35714rem 0 0 .35714rem;
    }
    .form__button{
      background-color: #24baef;
      //margin-right: 130px;
      border-color: #24baef;
      border-right: none;
      font-weight: 600;
      padding: 10px 15px;
      color: #fff;
      border-radius: 0 .35714rem .35714rem 0;
      text-transform: uppercase;
    }
    .form__method{
      width: 130px;
      padding: 5px 5px;
      border: none;
      color: #fff;
      font-weight: 600;
      background-color: #24baef;
      text-transform: uppercase;
    }
    .form__method__item{
      padding: 12px 11px;
      background-color: #24baef;
      height: 30px;
    }
  }
  .search__users__list{
    width: 80%;
    height: auto;
    margin: auto;
  }
  .table{
    margin: 40px auto;
    width: 100%;

    table{
      margin: auto;
      border: 2px solid #fff;
    }
  }
}

@media (max-width:992px) {
}

@media (max-width:768px) {

}

@media (max-width:425px) {
  
 
}

</style>