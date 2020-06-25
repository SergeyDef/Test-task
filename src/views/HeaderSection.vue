<template lang="pug">
  .search
    h1.search__title {{ title }}
    button( v-on:click="getUsers" ).search__button request a list
    .search__form.form
      input.form__input#search
      button( v-on:click="searchUser" ).form__button search
    .search__users__list.table
      table
        tr.table__line
          td.table__cell
            span.table__header photo
          td.table__cell
            span.table__header name
          td.table__cell
            span.table__header id
        element-table( 
          v-for="user in users"
          :key="user.id"
          v-bind:user_data="user"
         )
</template>

<script>
import ElementTable from '@/components/ElementTable';

export default {
  name: "search-users",
  components: {
    ElementTable
  },
  data() {
    return {
      title: 'find and sort users',
      users: [
        {
          id:1, 
          friendName:"Марина", 
          avatarSrcFriend:"https://avatars.mds.yandex.net/get-pdb/1936494/b54ac088-fa39-4f4f-b8dd-1d387da466ae/s1200"
        },
        {
          id:2, 
          friendName:"Валерия", 
          avatarSrcFriend:"https://yt3.ggpht.com/a/AATXAJyeElqaUFj1Orn19o0Ux-EHBnPkx1sqqtaK8g=s900-c-k-c0xffffffff-no-rj-mo"
        },
        {
          id:3, 
          friendName:"Lenka", 
          avatarSrcFriend:"https://yt3.ggpht.com/a/AGF-l78G1OYVfx10MRsHr3tzTjQ_FFMM6nt_cjiZzQ=s900-c-k-c0xffffffff-no-rj-mo"
        },
        {
          id:4, 
          friendName:"Алексей", 
          avatarSrcFriend:"https://img3.badfon.ru/wallpaper/big/3/2d/devushka-lico-elf-vzglyad-7450.jpg"
        },
        {
          id:5, 
          friendName:"Катя", 
          avatarSrcFriend:"https://i.pinimg.com/originals/8a/ec/c4/8aecc4b99cf3f2cf1ddd0052f934a527.jpg"
        },
        {
          id:6, 
          friendName:"Ленка", 
          avatarSrcFriend:"https://i.pinimg.com/originals/45/34/8c/45348c6e37956ee991a3ebd845e4d762.jpg"
        },
        {
          id:7, 
          friendName:"Пётр", 
          avatarSrcFriend:"https://i.pinimg.com/736x/99/1b/91/991b9187e4b6cbf0d0e2a170e04b6ceb.jpg"
        },
              {
          id:8, 
          friendName:"Елена", 
          avatarSrcFriend:"https://pbs.twimg.com/media/Drx3N9eU8AEXgjW.jpg"
        },
        {
          id:9, 
          friendName:"Тытьяна", 
          avatarSrcFriend:"https://i.ytimg.com/vi/iAU8yKY9tAY/maxresdefault.jpg"
        }
      ]
    };
  },
  methods: {
    getUsers: function () {
      
      let xhr = new XMLHttpRequest();

      xhr.open("GET", "https://raw.githubusercontent.com/SergeyDef/nitrenJSON-/master/friends_profile.json");

      xhr.send()

      xhr.responseType = "json"
      
      xhr.onload = function() {
        //let obj = xhr.response.items
        //let us = obj.slice()
        //console.log(us)
      }
      console.log(this.users)
    },
    searchUser: function(){
      let input = document.getElementById('search');

      let test = [1, 5, 8, 9, 4].filter(function(item){
        item == +input.value
      });

      console.log(test);
      
      let results = this.users.filter(function(item){
        item.id == +input.value
        console.log(item.id == +input.value)
      });

      console.log(results);
      console.log(input.value);
    },
  }
}

</script>
<style lang="scss" >

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
      border-color: #24baef;
      border-radius: 0 .35714rem .35714rem 0;
      font-weight: 600;
      padding: 10px 15px;
      color: #fff;
      text-transform: uppercase;
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