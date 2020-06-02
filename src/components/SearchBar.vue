<template>
  <div>
     <input @keypress.enter="onInput" type="text" placeholder="검색어를 입력하세요.">
  </div>
</template>

<script>
export default {
   name: 'SearchBar',
   methods: {
       onInput(e) {
           console.log(e)
           this.$emit('inputChange', e.target.value)
       }
   }
}
</script>

<style scoped>
    input {
        width: 80%;
        border: 2px solid black;
        border-radius: 4px;
        height: 50px;
        font-size: 20px;
        padding: 5px 10px 5px 10px;
    }
    div {
        text-align: center;
        margin: 20px;
    }
</style>