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
        tr.table__header
          td.table__cell
            span.table__header__text photo
          td.table__cell
            span.table__header__text name
          td.table__cell
            span.table__header__text surname
          td.table__cell
            span.table__header__text id
        element-table( 
          v-for="user in usersCopy"
          :key="user.id"
          v-bind:user_data="user"
          v-on:choose="chooseInfoWindow"
         )
    info-button( 
      v-if="infoIndicator" 
      v-on:hide="hideInfoWindow"
      v-for="userInfo in infoWindow"
      :key="userInfo.id"
      v-bind:user_info="userInfo"
      )
    popup-link(
      v-if="informationIndicator"
      v-on:hideInfo="hideAnswer"
      v-for="answer in infoAnswer"
      :key="answer.id"
      v-bind:info_answer="answer"
      )
</template>

<script>
import InfoWindow from '@/components/InfoWindow';
import ElementTable from '@/components/ElementTable';
import InfoButton from '@/components/InfoButton';
import PopupLink from '@/components/PopupLink';
import * as axios from 'axios';

export default {
  name: "search-users",
  components: {
    ElementTable,
    InfoWindow,
    InfoButton,
    PopupLink,
  },
  data() {
    return {
      title: 'find and sort users',
      users: [],
      usersCopy: null,
      info: null,
      infoIndicator: false,
      infoWindow: null,
      informationIndicator: false,
      infoAnswer: [
        {
          id:1,
          answerInfo: null,
        }
      ],
    };
  },
  mounted() {
    axios
      .get('https://raw.githubusercontent.com/SergeyDef/nitrenJSON-/master/users_search.json')
      .then(response => (this.users = response.data.items))
      .catch(error => alert(error))
      .finally( () => ( this.usersCopy = this.users.slice() ) )
  },
  methods: {
    getUsers: function () {
      console.log(this.usersCopy)
    },
    searchUser: function(){
      let input = document.getElementById('search');

      if (input.value == "" || input.value == " ") {
        this.informationIndicator = true
        this.infoAnswer[0].answerInfo = "You entered an empty string! Enter a query."  

      } else if (input.value != "" || input.value != " "){

        let results = this.users.filter(function(item){
        return item.id === +input.value ||
        item.firstName.toLowerCase() === input.value.toLowerCase() || 
        item.lastName.toLowerCase() === input.value.toLowerCase();
      });
        if (results.length === 0 ) {
          this.usersCopy = this.users 
          this.informationIndicator = true
          this.infoAnswer[0].answerInfo = "The user is not found. Repeat the request."
        } else{
          this.usersCopy = results
        }
      }
    },
    chooseInfoWindow: function (id){
      this.infoWindow = this.users.filter(item => item.id === id )
      this.infoIndicator = true
    },
    hideInfoWindow: function (){
      this.infoIndicator = false
    },
    hideAnswer: function (){
      this.informationIndicator = false
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

  &__title{
    text-transform: uppercase;
    padding: 30px 0;
  }

  &__button{
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

  &__form{
    width: 100%;
    height: auto;
  }

  &__users__list{
    width: 80%;
    height: auto;
    margin: auto;
  }

  .form{

    &__input{
      width: 550px;
      height: 35px;
      border-color: #24baef;
      border-radius: .35714rem 0 0 .35714rem;
    }
    &__button{
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
    &__method{
      width: 130px;
      padding: 5px 5px;
      border: none;
      color: #fff;
      font-weight: 600;
      background-color: #24baef;
      text-transform: uppercase;
    }
    &__method__item{
      padding: 12px 11px;
      background-color: #24baef;
      height: 30px;
    }
  }
  .table{
    margin: 40px auto;
    width: 100%;

    table{
      margin: auto;
      border: 2px solid #fff;
    }

    &__header{
      background-color: #000;
    }

    &__header__text{
      font-size: 25px;
      font-weight: 900;
      text-transform: uppercase;
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