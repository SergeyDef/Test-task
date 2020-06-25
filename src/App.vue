<template lang="pug">
  #app
    header-section()
</template>

<script>
import { HeaderSection } from "@/views"

export default {
  name: "app",
  components: {
    HeaderSection
  },
   data() {
    return {
      
    };
  },
  methods: {
  }
}
</script>

<style lang="scss">
@import "~@/scss/fonts.scss";
@import "~@/scss/mixins.scss";
@import "~@/scss/variables.scss";

*{
  margin: 0;
  padding: 0;
}

#app {
  @include baseText();
  text-align: center;
}

.title-with-line {
  @include baseText(Bold, 36px);
  text-transform: uppercase;
  text-align: left;

  &__line {
    width: 100%;
    height: 8px;
    background-color: $mainTextColor;
    margin-top: 21px;
  }
}

@media (max-width:425px) {
  .title-with-line {
    font-size: 18px;
    
    &__line {
      height: 4px;
      margin-top: 10px;
     
    }
  }
}

</style>
