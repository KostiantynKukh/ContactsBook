<template>
  <div class="wrapper">    
    <contacts-list />
  </div>
</template>

<script>
import ContactsList from "@/components/ContactsList"

export default {
  name: 'Home',
  components: {
    ContactsList,
  }  
}
</script>

<style scoped lang="scss">
.wrapper {
  max-width: 480px;
  margin: 50px auto;
}
</style>
