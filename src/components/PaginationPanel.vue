<template>
  <div class="pagination__panel">
    <button id="prevBtn" @click="selectPage--" :disabled="selectPage <= 1">Назад</button>
    <div class="page__wrap">
      <button @click="selectPage = page" v-for="page in calPage" :key="page"
      :class="{
        activePage: selectPage == page
      }">
        {{ page }}
      </button>
    </div>
    <button id="nextBtn" @click="selectPage++" :disabled="selectPage >= postsLength / amountItemForPage">Вперёд</button>
  </div>
</template>

<script>
export default {
  name: 'PaginationPanel',
  props: {
    postsLength: {
      type: Number,
      required: false,
    },
    amountItemForPage: {
      type: Number,
      required: true
    }
  },
  data(){
    return {
      selectPage: 1
    }
  },
  methods: {
    selectedPage(page) {
      this.selectPage = page
    },
  },
  computed: {
    calPage() {
      let localArray = []
      const currentPage = Math.ceil(this.postsLength / this.amountItemForPage)
      for(let i = 1; i <= currentPage; i++){
        localArray.push(i)
      }
      return localArray
    }
  },
  watch: {
    selectPage(){
      this.$emit('selectedPage', this.selectPage)
    }
  }
}
</script>

<style scoped lang="scss">

@import '../assets/main.scss';
.pagination__panel {
  justify-content: space-between;
  display: grid;
  grid-template-columns: repeat(3, auto);

  .page__wrap {
    button {
      padding: 0 7px;
      font-style: italic;
      
    }
  }
  button{
    background: none;
    border: none;
    cursor: pointer;
    user-select: none;
    width: auto;
    color: $mainColor;
    transition: all ease-in-out 0.2s;
  }

  .activePage{
    color: #7EBC3C;
  }

  button:disabled{
    opacity: 0.3;
  }

  #prevBtn, #nextBtn {
    padding: 0px 45px;
    font-weight: 500;
    &:active {
      transform: scale(1.2);
    }
  }
}

@import '../assets/mainMedia';
</style>
