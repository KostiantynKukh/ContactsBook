<template>
  <div class="contacts-list__wrapper">
    <h2 class="contacts-list_title">Contacts book</h2>   
    
    <add-contact-popup 
      v-if="popupIsActive"
      @cancelAdding="cancelAdding"
      @addingContact="addingContact"      
      >
    </add-contact-popup>

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

export default {
  name: 'ContactsList',
  components: {
    Contact,
    AddContactPopup
  },
  data() { 
    return {
      popupIsActive: false,
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
    removeContact(index) {
      this.contacts.splice(index, 1)
    },
    openAddContactPopup() {
      this.popupIsActive = true
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
        this.popupIsActive = false

      } else {
        this.popupIsActive = false
      }

    },
    cancelAdding() {
      this.popupIsActive = false
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
    background: rgb(63, 81, 248);
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