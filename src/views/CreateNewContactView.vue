<template>
    <div class="../views/CreateNewContactView.vue">
      <h1 class="text-white">This is a create new contact page</h1>
      
      <div class="container mt-5">
        <div class="row">
          <div class="col-md-4">
            <form @submit.prevent="submitCreate()">
              <div class="mb-2">
                <input required v-model="contact.name" type="text" class="form-control" placeholder="First Name">
              </div>
              <div class="mb-2">
                <input required v-model="contact.lastname" type="text" class="form-control" placeholder="Last Name">
              </div>
              <div class="mb-2">
                <input required v-model="contact.mobile" type="text" pattern="[0-9]*" class="form-control" placeholder="Mobile">
              </div>
              <div class="mb-2">
                <input required v-model="contact.email" type="email" class="form-control" placeholder="Email">
              </div>
              <div class="row">
                <div class="col-2">
                <input type="submit" class="btn btn-success" value="Save">
              </div>
              <div class="col-2">
                <input type="reset" class="btn btn-success" value="Clear">
              </div>
              <div class="col-3">
                <router-link to="/" class="btn btn-success"><i class="fa fa-arrow-alt-circle-left"></i> Back</router-link>
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
  name: "CreateNewContactView",
  data : function(){
    return {
      contact : {
        name : '',
        lastname : '',
        mobile : '',
        email : ''
      }
    }
  },
  methods : {
    submitCreate : async function(){
      ContactService.createContact(this.contact);
      this.$router.push('/create');
      
      
    }
  }
    

}

</script>
  