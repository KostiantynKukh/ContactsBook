<template>
  <div class="contact">
    <div class="contact_name">
      <span class="contact_first-name">{{ firstName }} </span> 
      <span class="contact_last-name"> {{ lastName }}</span>
    </div>
    <span class="contact_remove-contact" @click="removeContact(index)">
      &#10008;
    </span>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  props: {
    contact: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  data() {
    return {  
      id: this.contact.id,    
      firstName: this.contact.firstName,
      lastName: this.contact.lastName
    }
  },
  methods: {
    removeContact(index) {
      this.$emit('removedContact', index)
    }
  }
}
</script>

<style lang="scss" scoped>
.contact {
  display: flex;
  width: 100%;
  justify-content: space-between;
  padding: 5px 10px;

  &:hover {
    cursor: pointer;
  }

  &_name {
    font-size: 1.8rem;
  }

  &_remove-contact {
    font-size: 1.6rem;
    padding: 2px 6px;
    border-radius: 50%;
    transition: 0.2s;
    color: red;

    &:hover {
      background: rgb(255, 85, 85);
      color: #fff;
    }    
  }
}
</style>