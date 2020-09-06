<template>
  <div class="popup__wrapper" @click="hidePopup">
    <form @submit.prevent="submit" class="popup">
      <h2 class="popup_title">Add a new contact</h2>
      
      <input class="popup_first-name" v-model="newContact.firstName" type="text" placeholder="First name">

      <input class="popup_last-name" v-model='newContact.lastName' type="text" placeholder="Last name">

      <input class="popup_phone-number" v-model="newContact.phoneNumber" type="text" placeholder="Phone number">
      
      <input class="popup_email" v-model="newContact.email" type="text" placeholder="Email">

      <div class="popup__group">

        <w-button class="popup_cancel" size="sm" color="dark" event="cancelAdding" @cancelAdding="cancelAdding" type="button">
          Cancel
        </w-button>

        <w-button type="submit" size="sm" color="light" >
          Save
        </w-button>  

      </div>
    </form>
  </div>
</template>

<script>
import WButton from '@/widgets/WButton'

export default {
  name: 'AddContactPopup',
  components: {
    WButton
  },
  data() {
    return {
      newContact: {
        firstName: '',
        lastName:'',
        phoneNumber:'',
        email:''
      }
    }
  },
  methods: {
    hidePopup(e) {      
      if(e.target.classList.contains('popup__wrapper')) {
        this.$emit('cancelAdding')
      }
    },
    submit() {
      this.$emit('addingContact', this.newContact)
    },
    cancelAdding() {
      this.$emit('cancelAdding')
    }
  }
}
</script>

<style lang="scss" scoped>
.popup__wrapper {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center; 
  background: rgba(126, 126, 126, 0.4);
  }

.popup {
  width: 480px;
  padding: 20px;
  background: #eceaea;
  min-height: 400px;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;

  &_title {
    font-size: 2rem;
  }  
  &_cancel {
    margin-right: 40px;
  }
}
input[type='text'] {
  width: 100%;
  padding: 5px 10px;
  font-size: 1.8rem;
  background: rgb(161, 161, 161);
  border: 1px solid rgb(97, 97, 97);
  border-radius: 10px ;
  outline: none;
  color: #fff;
  text-align: center;
  
  &::placeholder {
    color: rgba(36, 36, 36, 0.774);
  }

  &:focus {
    border: 1px solid rgb(85, 85, 85);
    background: darken($color: rgb(149, 149, 149), $amount: 20);
  }
}
input[type='submit'], input[type='button'] {
    background: rgb(34, 48, 255);
    padding: 5px 10px;
    border-radius: 5px;
    font-size: 1.8rem;
    color: #fff;
    cursor: pointer;
    outline: none;
    transition: .2s;

    &:hover {
      background: lighten($color: rgb(34, 48, 255), $amount: 10);
      color: black;
    }
}

</style>