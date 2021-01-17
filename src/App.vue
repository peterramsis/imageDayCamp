<template>
  <div id="app">
     <div class="container">
     <form class="splash-container" method="POST" enctype="multipart/form-data" @submit.prevent="sendData">
         <div class="card register">
            <div class="card-header">
                <h3 class="mb-1">Registrations Form</h3>
                <p>Please enter your user information.</p>
            </div>
            <div class="card-body">
                <div class="form-group">
                    <input class="form-control form-control-lg" type="text" name="first_name" v-model="formData.first_name"  placeholder="First Name" >
                </div>
                <div class="form-group">
                    <input class="form-control form-control-lg" type="text" name="second_name" v-model="formData.second_name"  placeholder="second Name" >
                </div>
                <div class="form-group">
                        <input class="form-control form-control-lg" type="text" name="last_name" v-model="formData.last_name"  placeholder="Last Name" >
                </div>
                 <div class="form-group">
                    <input class="form-control form-control-lg" type="text" name="family_name" v-model="formData.family_name"  placeholder="family Name" >
                </div>
                    <div class="form-group">

                        <label for="username" class="cols-sm-2 control-label">Birthday</label>
                            <div class="cols-sm-10">
                                <div class="input-group">
                                        <input class="form-control form-control-lg" type="date" name="birthday" placeholder="Your birthday"  v-model="formData.birthday">
                                </div>
                            </div>
                    </div>


                    <div class="form-group">
                            <label for="username" class="cols-sm-2 control-label">Image profile</label>
                            <div class="cols-sm-10">
                                <div class="input-group">
                                    <input type="file" class="form-control" placeholder="Image profile" ref="file" @change="onImageChange">
                                </div>
                            </div>
                        </div>
                <div class="form-group">
                    <input class="form-control form-control-lg" type="text" name="username"  placeholder="Username" v-model="formData.username">
                </div>
                <div class="form-group">
                    <label for="username" class="cols-sm-2 control-label">Email</label>
                    <div class="cols-sm-10">
                                <div class="input-group">
                    <input class="form-control form-control-lg" type="email" name="email" placeholder="Email" v-model="formData.email">
                    </div>
                    </div>
                    
                </div>
                <div class="form-group">
                    <input class="form-control form-control-lg" id="password" type="password"  placeholder="Password" name="password" v-model="formData.password">
                </div>
                <div class="form-group">
                    <input class="form-control form-control-lg" placeholder="Confirm" name="password_confirmation" type="password" v-model="formData.password_confirmation">
                </div>

             
                
                
           <div class="form-group">

                <select name="school" class="form-control" v-model="formData.school">
                    <option value="">school</option>
                    <option value="1">Yes</option>
                    <option value="0">No</option>
                </select>
        </div>
        
          <div class="form-group">

                <select name="collage" class="form-control" v-model="formData.collage">
                    <option value="">collage</option>
                    <option value="1">Yes</option>
                    <option value="0">No</option>
                </select>
        </div>




            <div class="form-group">

                <select name="graduate" class="form-control" v-model="formData.graduate">
                    <option value="">Graduated</option>
                    <option value="1">Yes</option>
                    <option value="0">No</option>
                </select>
        </div>
        
         <div class="form-group" >
                    <input class="form-control form-control" placeholder="phone number" name="phone" type="number" min="11" v-model="formData.phone">
                </div>
        
        
          
        



                <div class="form-group pt-2">
                    <button class="btn btn-block btn-primary" type="submit">Register</button>
                </div>

    </div>
     </div>
     </form>
  </div>
  </div>
</template>

<script>
import axios from 'axios';
import { Form } from 'vform';
// axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';
export default {
  name: "App",
  data(){
      return{
         formData: new Form({
             first_name:"",
          last_name:"",
          second_name:"",
          family_name:"",
          birthday:"",
          username:"",
          email:"",
          password:"",
          password_confirmation:"",
          school:"",
          collage:"",
          graduate:"",
          phone:"",
          id_number:13492842398,
          dept_id: 2,
          ar_name:"بيتر رمسيس",
          image:""
         }),
        avatar: null,
        avatarName: null,
      }
  },
  methods:{
      sendData(){
        
      
         console.log(this.formData);

          axios.post("http://127.0.0.1:8000/api/v1/user",this.formData).then((result)=>{
              console.log(result);
          }).catch((err)=>{
              console.log(err)
          });
      },
       onImageChange(e) {
                let files = e.target.files || e.dataTransfer.files;
                if (!files.length)
                    return;
                this.createImage(files[0]);
            },
            createImage(file) {
                let reader = new FileReader();
                let vm = this;
                reader.onload = (e) => {
                    vm.formData.image = e.target.result;
                    console.log( vm.formData.image)
                };
                reader.readAsDataURL(file);
            }
  }
};
</script>
