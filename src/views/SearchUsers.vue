<template lang="pug">
  .search
    h1.search__title {{ title }}
    button( v-on:click="getUsers" ).search__button refresh list
    .search__form.form
      .form__clear( v-on:click="clearForm")
        span.clear
      input( 
        v-model="request" 
        placeholder="Enter the query: first name, last name, or user ID"  
        v-on:keyup.enter="searchUser" 
        ).form__input#search
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
            nav.table__sort.sort#name__sort( v-on:click="showOptions")
              .sort__pointer
            ul( v-if="sortName" v-on:click="sortArray" ).table__sort__option
              li.alphabet alphabetically
              li.order reverse order
          td.table__cell
            span.table__header__text surname
            nav.table__sort.sort#surname__sort( v-on:click="showOptions")
              .sort__pointer
            ul( v-if="sortSurname" v-on:click="sortArray" v-on:onblur="hideSort" ).table__sort__option
              li.alphabet alphabetically
              li.order reverse order
          td.table__cell
            span.table__header__text id
            nav.table__sort.sort#id__sort( v-on:click="showOptions")
              .sort__pointer
            ul( v-if="sortId" v-on:click="sortArray" ).table__sort__option
              li.order reverse order
              li.moreLess from more to less
              li.lessMore from less to more
        element-table( 
          v-for="user in usersCopy"
          :key="user.id"
          v-bind:user_data="user"
          v-on:choose="chooseInfoWindow"
         )
    info-message( 
      v-if="infoIndicator" 
      v-on:hide="hideInfoWindow"
      v-for="userInfo in infoWindow"
      :key="userInfo.id"
      v-bind:user_info="userInfo"
      )
    info-message(
      v-if="informationIndicator"
      v-on:hide="hideAnswer"
      v-for="answer in infoAnswer"
      :key="answer.id"
      v-bind:user_info="answer"
      )
    disabled-pages(
      v-if="disabledActive" 
      )
</template>

<script>
import ElementTable from '@/components/ElementTable';
import InfoMessage from '@/components/InfoMessage';
import DisabledPages from '@/components/DisabledPages';
import * as axios from 'axios';

export default {
  name: "search-users",
  components: {
    ElementTable,
    InfoMessage,
    DisabledPages,
  },
  data() {
    return {
      title: 'find and sort users',
      users: [],
      request: "",
      usersCopy: null,
      info: null,
      infoIndicator: false,
      infoWindow: null,
      informationIndicator: false,
      disabledActive: false,
      sortName: false,
      sortSurname: false,
      sortId: false,
      indicatorSort: null,
      infoAnswer: [
        {
          id:1,
          answerInfo: null,
          sensor: true
        }
      ],
    };
  },
  mounted() {
    this.disabledActive = true
    axios
      .get('https://raw.githubusercontent.com/SergeyDef/nitrenJSON-/master/users_search.json')
      .then(response => (this.users = response.data.items))
      .catch(error => alert(error))
      .finally( () => ( 
        this.usersCopy = this.users.slice(),
        this.disabledActive = false
        ) )
  },
  methods: {
    getUsers: function () {
      this.disabledActive = true
      axios
      .get('https://raw.githubusercontent.com/SergeyDef/nitrenJSON-/master/users_search.json')
      .then(response => (this.users = response.data.items))
      .catch(error => alert(error))
      .finally( () => ( 
        this.usersCopy = this.users.slice(),
        this.disabledActive = false
         ) )
    },
    searchUser: function(){
      let request = this.request

      if (request == "" || request == " ") {
        this.informationIndicator = true
        this.infoAnswer[0].answerInfo = "You entered an empty string! Enter a query."  

      } else if (request != "" || request != " "){
        let results = this.users.filter(function(item){
        return item.id === +request ||
        item.firstName.toLowerCase().includes(request.toLowerCase()) || 
        item.lastName.toLowerCase().includes(request.toLowerCase());
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
      this.infoWindow[0].sensor = false
      this.infoIndicator = true
    },
    hideInfoWindow: function (){
      this.infoIndicator = false
    },
    hideAnswer: function (){
      this.informationIndicator = false
    },
    clearForm: function (){
      this.request = ""
    },
    showOptions: function (){
      let id_elem = event.target.closest('nav').getAttribute('id')

      this.indicatorSort = id_elem
      
      switch(id_elem) {
        case 'name__sort':
          this.sortName = true
          this.sortSurname = false
          this.sortId = false
          break
        case 'surname__sort':
          this.sortSurname = true
          this.sortName = false
          this.sortId = false
          break
        case 'id__sort':
          this.sortId = true
          this.sortName = false
          this.sortSurname = false
          break
        default:
          alert("Something went wrong! Contact your administrator.")
      }
    },
    sortArray: function (){
      let option_sort = event.target.getAttribute('class')

      console.log(this.indicatorSort)
      console.log(option_sort)
      
      if (this.indicatorSort == 'name__sort' && option_sort == 'alphabet') {

        this.usersCopy.sort(( a, b ) =>{
          if (a.firstName.toLowerCase() > b.firstName.toLowerCase()) {
            return 1
          }
          if (a.firstName.toLowerCase() < b.firstName.toLowerCase()) {
            return -1
          }
           if (a.firstName.toLowerCase() == b.firstName.toLowerCase()) {
            return 0
          }
        })

        this.sortName = false

      } else if (this.indicatorSort == 'name__sort' && option_sort == 'order') {

        this.usersCopy.reverse()
        this.sortName = false

      } else if (this.indicatorSort == 'surname__sort' && option_sort == 'alphabet') {

        this.usersCopy.sort(( a, b ) =>{
          if (a.lastName.toLowerCase() > b.lastName.toLowerCase()) {
            return 1
          }
          if (a.lastName.toLowerCase() < b.lastName.toLowerCase()) {
            return -1
          }
           if (a.lastName.toLowerCase() == b.lastName.toLowerCase()) {
            return 0
          }
        })

        this.sortSurname = false

      } else if (this.indicatorSort == 'surname__sort' && option_sort == 'order') {

        this.usersCopy.reverse()
        this.sortSurname = false

      } else if (this.indicatorSort == 'id__sort' && option_sort == 'order') {

        this.usersCopy.reverse()
        this.sortId = false
      } else if (this.indicatorSort == 'id__sort' && option_sort == 'lessMore'){

        this.usersCopy.sort(( a, b ) =>{
          if (a.id > b.id) {
            return 1
          }
          if (a.id < b.id) {
            return -1
          }
           if (a.id == b.id) {
            return 0
          }
        })

        this.sortId = false

      } else if (this.indicatorSort == 'id__sort' && option_sort == 'moreLess'){

        this.usersCopy.sort(( a, b ) =>{
          if (a.id < b.id) {
            return 1
          }
          if (a.id > b.id) {
            return -1
          }
           if (a.id == b.id) {
            return 0
          }
        })

        this.sortId = false

      }
    },
    hideSort: function() {
      this.sortName = false
      this.sortSurname = false
      this.sortId = false
    }
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
    display: flex;
    justify-content: center;

    &__input{
      margin-left: 7px;
      width: 550px;
      height: 35px;
      padding-left: 5px;
      font-size: 18px;
      background-color: #ffffff;
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

    &__clear{
      position: relative;
      display: inline-block;
      margin-top: 7px;
      width: 25px;
      height: 25px;
      background-color: #24baef;
      opacity: 0.4;
      border-radius: 20px;
      cursor: pointer;

      .clear{
        position: absolute;
        right: 18%;
        top: 10%;
        width: 25px;
        height: 25px;
      }
      .clear:before, .clear:after{
        position: absolute;
        left: 15px;
        content: ' ';
        height: 20px;
        width: 3px;
        background-color: #fff;
      }
      .clear:before{
        transform: rotate(45deg);
      }
      .clear:after{
        transform: rotate(-45deg);
      }
    }
    &__clear:hover{
      opacity: 0.9;
    }
  }
  .table{
    margin: 40px auto;
    width: 100%;
    position: relative;

    table{
      margin: auto;
      border: 2px solid #fff;
      box-shadow: 0 24px 48px rgba(0,0,0,0.25), 0 20px 20px rgba(0,0,0,0.22);
    }

    &__header{
      background-color: #000;
    }

    &__header__text{
      font-size: 25px;
      font-weight: 900;
      text-transform: uppercase;
    }
    .table__sort{
      position: absolute;
      width: 50px;
      height: 20px;
      border-radius: 10px;
      background-color: #666666;
      border: 1px solid #fff;
      cursor: pointer;
    }
    .sort{

      &__pointer{
        width: 20px;
        height: 20px;
        margin: auto;
      }
      &__pointer:after{
        content: ''; 
        position: absolute;
        left: 13px; bottom: -5px;
        border: 10px solid transparent;
        border-top: 10px solid #fff;
      }
    }
    &__sort__option{
      position: absolute;
      margin-left: 0;
      padding-left: 0;
      top: 65px;

      li{
        background-color: #000;
        list-style: none;
        width: 250px;
        border: 1px solid #fff;
        font-size: 16px;
        padding: 5px 0;
        cursor: pointer;
      }
      li:hover{
        color: #24baef;
        background-color: #333333;
      }
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