<template>
  <div class="contacts-list__wrapper">
    <h2 class="contacts-list_title">Contacts book</h2>   
    
    <add-contact-popup 
      v-if="popupAddContactIsVisible"
      @cancelAdding="cancelAdding"
      @addingContact="addingContact"      
      >
    </add-contact-popup>
    
    <confirmation-remove-popup
    v-if="popupConfirmationRemoveIsVisible"   
    @confirmationRemove="confirmationRemove"
    >
    {{ removingContactInfo.contact.firstName }}
    {{ removingContactInfo.contact.lastName }}    
    </confirmation-remove-popup>
    

    <div class="contacts-list">
      <button class=contacts-list_add-contact
      @click="openAddContactPopup"
      >
      +
    </button>

      <contact v-for="(contact, index) in contacts" :key="contact.id" :contact='contact' :index='index' @removedContact="removeContact" class="contacts-list_item">      
      </contact>
    </div>  
  </div>
  
</template>

<script>
import Contact from '@/components/Contact'
import AddContactPopup from '@/components/popups/AddContactPopup'
import ConfirmationRemovePopup from '@/components/popups/ConfirmationRemovePopup'

export default {
  name: 'ContactsList',
  components: {
    Contact,
    AddContactPopup,
    ConfirmationRemovePopup
  },
  data() { 
    return {
      popupAddContactIsVisible: false,
      popupConfirmationRemoveIsVisible: false,
      removingContactInfo: '',
      idForContact: 4,
      contacts: [
        {
          id: 1, 
          firstName: 'John',
          lastName: 'Smith',
          phoneNumber: '+380971234567',
          email: 'example@example.com'

        },
        { 
          id: 2,
          firstName: 'David',
          lastName: 'Jones',
          phoneNumber: '+380971234567',
          email: 'example@example.com'
        },
        { 
          id: 3,
          firstName: 'Michael',
          lastName: 'Johnson',
          phoneNumber: '+380971234567',
          email: 'example@example.com'
        }      
      ]
    }
  },
  methods: {    
    removeContact(data) {
      this.popupConfirmationRemoveIsVisible = true
      this.removingContactInfo = data
    },
    confirmationRemove(state) {      
      state ? this.contacts.splice(this.removingContactInfo.index, 1) : this.popupConfirmationRemoveIsVisible = false
      this.popupConfirmationRemoveIsVisible = false
    },
    openAddContactPopup() {
      this.popupAddContactIsVisible = true
    },
    addingContact(contact) {
      if((contact.firstName || contact.lastName) && contact.phoneNumber) {
        this.contacts.push({
          id: this.idForContact,
          firstName: contact.firstName,
          lastName: contact.lastName,
          phoneNumber: contact.phoneNumber,
          email: contact.email
        })
        this.idForContact++
        this.popupAddContactIsVisible = false

      } else {
        this.popupAddContactIsVisible = false
      }

    },
    cancelAdding() {
      this.popupAddContactIsVisible = false
    }
  } 
}
</script>

<style lang="scss" scoped>
.contacts-list {
  width: 100%;  
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;;

  &_title {
    font-size: 3rem;
    margin-bottom: 20px;
    text-align: center;
  }

  &_add-contact {     
    background: #111B47;
    color: #fff;
    font-size: 3rem;
    padding: 5px 12px;
    border-radius: 50%;
    text-align: center;
    cursor: pointer;
    transition: 0.2s;
    margin: 10px 0;
    outline: none;
    
    &:hover {
      background: darken($color: rgb(63, 81, 248), $amount: 20);
    }
  }
}

.contacts-list_item {
  margin: 5px 0;
}
</style>