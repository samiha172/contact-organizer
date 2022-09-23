<template>
    <div class="contacts">
      <h1 class="text">Contact Organizer</h1>
      <br>
      <form>
        
             <div class="container mt-5">
               <input type="text" class="form-control" placeholder="Search First Name" v-model="filterInput">
             </div>
             <br />
           
          
        
      </form>
      
      <div class="container mt-5" v-if="contacts.length > 0">
       <div class="row">
        <div class="col-md-4" v-for="contact of filterBy(contacts, filterInput)" :key="contact">
          <div class="card my-2 list-group-item-dark shadow-lg">
            <div class="card-body">
              <div class="row align-items-center">
                <div class="col-sm">
                  <ul class="list-group">
                    <li class="list-group-item">First Name : <span class="fw-bold">{{contact.name}} {{contact.lastname}}</span></li>
                    <li class="list-group-item">Mobile : <span class="fw-bold">{{contact.mobile}}</span></li>
                    <li class="list-group-item">Email : <span class="fw-bold">{{contact.email}}</span></li>
                    
                    <RouterLink :to="`/contacts/edit/${contact.id}`" class="btn btn-primary my-1">
                    <i class="fa fa-pen"></i>
                    </RouterLink>
                    <button class="btn btn-danger my-1" @click="clickDeleteContact(contact.id)">
                    <i class="fa fa-trash"></i>
                    </button>
                  </ul>
                </div>
                
              </div>
            </div>

          </div>
         </div>
       </div>
      </div>
    </div>
    
  </template>

<script>
import { ContactService } from '@/services/ContactService';

   export default {
    name: "ContactListView",
    data : function() {
      return {
        loading : false,
        contacts : [],
        errorMessage : null,
        filterInput : ''
      }
    },
    created : async function() {
      try {
        let response = await ContactService.getAllContacts()
        this.contacts = response.data;
      }
      catch(error){
        this.errorMessage = error;
      }

    },
    methods : {
      clickDeleteContact : async function(contactId){
        try {
          let response = await ContactService.deleteContact(contactId);
          if(response){
            let response = await ContactService.getAllContacts();
            this.contacts = response.data;
          }
        }
        catch(error) {
          this.errorMessage = error;
          
        }
      },
      filterBy(list, value){
        value = value.charAt(0).toUpperCase() + value.slice(1);
        return list.filter(function(contact){
          return contact.name.indexOf(value) > -1;
        });
      }
      }
    }
   
  
    
  </script>
  
  <style scoped>
    
  </style>
  