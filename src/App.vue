<template>
  <div>
  <div class="root">
    <h2 style="text-align:center">User Details</h2>
    <p>
      <input type="text" placeholder="First Name" v-model="fname"/>
    </p>
    <p>
      <input type="text" placeholder="Last Name" v-model="lname"/>
    </p>
    <p>
      <input type="text" placeholder="Email" v-model="email"/>
    </p>
    <p>
      <input type="numeric" placeholder="Phone" v-model="phone"/>
    </p>
    <button @click="submitForm">Submit</button>
  </div>
  <div style="text-align:center"> 
      Total No. of Records = {{ this.allUsers.length }}
    </div>
      <div>
          <table border="1|0" class="centered">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">First Name</th>
                <th scope="col">Last Name</th>
                <th scope="col">Email</th>
                <th scope="col">phone</th>
            </tr>
            </thead>
            <tbody>
              <tr v-for="(user, i) in allUsers" :key="i">
                <th scope="row">{{ ++i }}</th>
                <td>{{ user.fname }}</td>
                <td>{{ user.lname }}</td>
                <td>{{ user.email }}</td>
                <td>{{ user.phone }}</td>
              </tr>
            </tbody>
            
          </table>
    </div>
</div>
</template>

<script>


export default {
  data() {
    return {
      fname: '',
      lname: '',
      email: '',
      phone:'',
      allUsers : [],
    }
  },
  methods : {
    validEmail(email)
    {
      let regex = /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(.\w{2,3})+$/ ;
      return regex.test(email);
    },
    validPhone(phone)
    {
      if( isNaN(phone) || phone.length !== 10)
      {
        return false;
      }
      return true;
    },
    validate()
    {
      if(this.fname === '')
      {
        alert('First Name is required')
        return false;
      }
      if(this.lname === '')
      {
        alert('Last Name is required')
        return false;
      }
      if(this.email === '')
      {
        alert('email is required')
        return false;
      }
      if(!this.validEmail(this.email))
      {
        alert('Not a valid email');
        return false;
      }
      if(this.phone === '')
      {
        alert('Mobile number is required');
        return false;
      }
      if(!this.validPhone(this.phone))
      {
        alert('Not a valid Mobile Number');
        return false;
      }
      return true;

    },
    submitForm() {
      let valid = this.validate() ;
      if (valid) {
        const allUsers = this.allUsers;
        const formEmail = this.email;
        const isFound = allUsers.some(element => element.email === formEmail)
        if(!isFound){
          this.allUsers.push({fname : this.fname, lname: this.lname, email:this.email, phone:this.phone});
          this.clearForm();
        }
        else{
          alert('User already exists');
        }
      }
    },
    
    clearForm() {
      this.fname = "";
      this.lname = "";
      this.email = "";
      this.phone = "";
    },
  }
}

</script>


<style lang="css">
.root {
  width: 500px;
  margin: 0 auto;
  background-color: #fff;
  padding: 30px;
  margin-top: auto;
  margin-left: auto;
  border-radius: 20px;
}
input {
  border: none;
  outline: none;
  border-bottom: 1px solid #ddd;
  font-size: 1em;
  padding: 5px 0;
  margin: 10px 0 5px 0;
  width: 100%;
}
button {
  background-color: #3498db;
  padding: 10px 20px;
  margin-top: 10px;
  border: none;
  color: white;
}
.centered{
  width: 70%;
  margin-left: auto;
  margin-right: auto;
  border: 1px solid #000;
  margin-top: 30px;
}


</style>

