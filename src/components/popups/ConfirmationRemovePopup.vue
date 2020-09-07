<template>
  <div class="remove-contact__wrapper" @click="hidePopup">
    <div class="remove-contact">
      <h3 class="remove-contact_title">Remove contact 
        <span class="remove-contact_name" ><slot/>?</span>         
      </h3> 
      <div class="remove-contact_button-group">
        <w-button size="md" color="dark" type="button" event="cancelRemove" @cancelRemove="cancelRemove">
          Cancel
        </w-button>
        <w-button size="md" color="light" type="button" event="confirmRemove" @confirmRemove="confirmRemove">
          Remove
        </w-button>
      </div>
    </div>
  </div>
</template>

<script>
import WButton from '@/widgets/WButton'

export default {  
  name: 'ConfirmationRemovePopup',
  components: {
    WButton
  },
  methods: {
    cancelRemove() {
      this.$emit('confirmationRemove', false)
    },
    confirmRemove() {
      this.$emit('confirmationRemove', true)
    },
    hidePopup(e) {      
      if(e.target.classList.contains('remove-contact__wrapper')) {
        this.$emit('confirmationRemove', false)
      }
    },
  }
}
</script>

<style lang="scss" scoped>
.remove-contact__wrapper {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: flex-end; 
  background: rgba(126, 126, 126, 0.4);  
}
.remove-contact {
  width: 480px;
  padding: 20px;
  background: #eceaea;
  min-height: 200px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;


  &_title {
    font-size: 2rem;
    color: rgb(87, 87, 87);
  }

  &_name {
    color: black;
    font-size: 2.2rem;
  }

  &_button-group {
    display: flex;
    width: 90%;
    justify-content: space-between;
  }
}
</style>