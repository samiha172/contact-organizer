<template>
    <RouterView/>
    <div class="../views/ViewContactView.vue">
      <h1 class="text-white">This is an edit contact page</h1>
      <div class="container mt-5">
        <div class="row">
          <div class="col-md-4">
            <form @submit.prevent="updateSubmit()">
              <div class="mb-2">
                <input v-model="contact.name" type="text" class="form-control" placeholder="First Name">
              </div>
              <div class="mb-2">
                <input v-model="contact.lastname" type="text" class="form-control" placeholder="Last Name">
              </div>
              <div class="mb-2">
                <input v-model="contact.mobile" type="text" pattern="[0-9]*" class="form-control" placeholder="Number">
              </div>
              <div class="mb-2">
                <input v-model="contact.email" type="email" class="form-control" placeholder="Email">
              </div>
              <div class="row">
              
              <div class="col-3">
                <router-link to="/contacts" class="btn btn-success"><i class="fa fa-arrow-alt-circle-left"></i> Back</router-link>
              </div>
              <div class="col-2">
                <input type="submit" class="btn btn-success" value="Update">
              </div>
            </div>
              
            </form>
          </div>
        </div>
      </div>
    </div>
    
  </template>

  <script>
import { ContactService } from '@/services/ContactService';

    export default{
      name : "EditContactView",
      data : function() {
        return {
          contactId : this.$route.params.contactId,
          loading : false,
          contact : {
          name : '',
          lastname : '',
          mobile : '',
          email : ''
          },
          errorMessage : null
        }
      },
      created : async function(){
        try{
          let response = await ContactService.getContact(this.contactId);
          this.contact = response.data;
        }
        catch(error){
          this.errorMessage = error;
        }
      },
      methods : {
        updateSubmit : async function(){
          try{
            let response = await ContactService.updateContact(this.contact, this.contactId);
            if(response){
              return this.$router.push('/contacts');
            }
            else {
              return this.$router.push(`/contacts/edit/${this.contactId}`);
            }
          }
          catch (error) {
            console.log(error);
          }
        }
      }
    }
  </script>
  