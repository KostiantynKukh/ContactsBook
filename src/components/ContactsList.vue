<template>
  <div class="contacts-list__wrapper">

    <!-- POPUPS START -->
    <add-contact-popup 
      v-if="isVisiblePopupAddContact"
      @onCancelAdd="cancelAdd"
      @onAddContact="addContact"      
    />
    
    
    <confirm-remove-popup
      v-if="isVisiblePopupConfirmRemove"   
      @onClickRemove="confirmRemoveContact(idOfRemovingContact)"
      @onClickCancel="cancelRemoveContact"
    >
      {{ fullNameOfRemoveContact }}
    </confirm-remove-popup> 

    <!-- POPUPS END -->

    <h2 class="contacts-list_title">Contacts book</h2>       

    <div class="contacts-list">
      <button 
        class=contacts-list_add-contact
        @click="isVisiblePopupAddContact = true"
      >
        +
      </button>

      <contact 
        v-for="contact in contacts"
        :key="contact.id"
        :contact='contact'         
        @onRemoveContact="removeContact"
        class="contacts-list_item"
      />      
      

    </div>  
  </div>
  
</template>

<script>
import Contact from '@/components/Contact'
import AddContactPopup from '@/components/popups/AddContactPopup'
import ConfirmRemovePopup from '@/components/popups/ConfirmRemovePopup'

export default {
  name: 'ContactsList',
  components: {
    Contact,
    AddContactPopup,
    ConfirmRemovePopup
  },
  data() { 
    return {
      isVisiblePopupAddContact: false,
      isVisiblePopupConfirmRemove: false,
      fullNameOfRemoveContact: '',
      idOfRemovingContact: '',
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
  // computed: {
  //   fullNameOfRemoveContact() {
  //     return removingContactInfo.contact.firstName +
  //     ' ' + 
  //     removingContactInfo.contact.lastName;

  //   },
  // },
  methods: {    
    removeContact(contact) {
      this.fullNameOfRemoveContact = contact.firstName +
      ' ' + contact.lastName
      this.idOfRemovingContact = contact.id
      this.isVisiblePopupConfirmRemove = true
    },
    confirmRemoveContact(id) { 
      this.contacts.splice(
      this.contacts.findIndex(item => item.id === id), 1)
      this.isVisiblePopupConfirmRemove = false
    },
    cancelRemoveContact () {
      this.isVisiblePopupConfirmRemove = false
    },
    openAddContactPopup() {
      this.popupAddContactIsVisible = true
    },
    addContact(contact) {
      if((contact.firstName || contact.lastName) && contact.phoneNumber) {
        this.contacts.push({
          id: this.idForContact,
          firstName: contact.firstName,
          lastName: contact.lastName,
          phoneNumber: contact.phoneNumber,
          email: contact.email
        })
        this.idForContact++
        this.isVisiblePopupAddContact = false

      } else {
        this.isVisiblePopupAddContact = false
      }

    },
    cancelAdd() {
      this.isVisiblePopupAddContact = false
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