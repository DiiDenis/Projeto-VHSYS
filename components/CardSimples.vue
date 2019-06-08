<template>
  <div 
    class="card-default">
    <slot/>
  </div>
</template>

<script>
export default {
  name: 'CardSimples',
  props: {
    
  },
  computed: {    
  }
}
</script>

<style lang="scss" scoped>

  .card-default {
    background-color: #FFFFFF;
    border-radius: 4px;
    padding: 28px;
    box-shadow: 0px 0px 10px 5px rgba(0, 0, 0, .12);
    margin-bottom: 28px;
    width: 100%;
  }

  

</style>