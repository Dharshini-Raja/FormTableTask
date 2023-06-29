  <template>
      <!-- <RouterLink to="/form"  v-if="hide">Forms</RouterLink> -->
      
      <form @submit.prevent="display">
        <h2>Student Details Form</h2><br>
      <input type="text" v-model="details.uname"  placeholder="Enter name"><br>
      <span id="err">{{ name }}</span><br>
      <input type="text" v-model="details.umobile"  placeholder="Enter mobile"><br>
      <span id="err">{{ mobile }}</span><br>
      <input type="text" v-model="details.utotal" placeholder="Enter total"><br>
      <span id="err">{{ total }}</span><br>
      <input type="email" v-model="details.uemail" placeholder="Enter email" required><br>
      <span id="err">{{ email }}</span><br>

<br><br>
<div id="submit">
      <button type="submit">{{ edit ?'Update':'Add' }}  </button>
</div>
      </form>
  
  </template>
    <script>
    export default {
      name: 'Form1',
      props: {
        initialData: Object,
      },
      data () {
          
          return{
             hide: false,
             myString: null,
              details:{
                  uname: null,
                  umobile: null,
                  utotal: null,
                  uemail: null
              },
              edit: false
             
          }
      },
      
      methods: {
          
          display(){
            const formData = {
              uname: this.details.uname,
              umobile: this.details.umobile,
              utotal: this.details.utotal,
              uemail: this.details.uemail
            };
            if(this.edit){
              this.$emit('editStudent',formData);
            }
            else{
             
               this.$emit('values',JSON.stringify(this.details));

              this.resetform();
            }
          },
          resetform(){
                  this.details.uname= "";
                  this.details.umobile= "";
                  this.details.utotal= "";
                  this.details.uemail= "";
  
  
          },
        
         
      },
      watch:{
        initialData(newData){
          if(newData){
            this.details.uname = newData.uname;
            this.details.umobile = newData.umobile;
            this.details.utotal = newData.utotal;
            this.details.uemail = newData.uemail;
            this.edit = true;
          }else{
            this.resetform();
            this.edit = false;
          }
        }
      },
      computed: {
        name() {
              this.myString = this.details.uname;
  
              if(this.myString==null){ return "Type in the name";}
              else if(this.myString.length<5) return "Type a bigger name!!"
              else{
                  for (let i=0; i<this.myString.length; i++) {
                      if (/[^A-Za-z]+$/.test(this.myString)) 
                          return 'Only alphabets allowed!!';
                      
                  }
              }
          },  
          mobile(){
              if(this.details.umobile == null) return "Type in the number";
              else{
                if(/[^0-9]/.test(this.details.umobile)) alert('Only numbers allowed');
                  if(this.details.umobile.length!=10) return "10 digits only!!";
                  
                  
              }
          },
          total(){
              if(this.details.utotal == null) return "Type in the number";
              else{
                  if(/[^0-9\.]/.test(this.details.utotal)) alert('Only floats allowed');
                  if(this.details.utotal>=0 && this.details.utotal<=100 ) return "Enter marks between 0 to 100" ;
                  
              }
          },
          email(){
              if(this.details.uemail == null) return "Type in the email";
              else{
              if (/^\w+([\.-]?\w+)*\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.details.uemail)) 
              return 'Please enter a valid email address';
              }
      
          },
      }
  }
    </script>
  <style>
 body {
  width: 100%;
  max-width: 68rem;
  margin: 0 auto;
  font: 1.6rem/1.25 "Helvetica Neue", Helvetica, Arial, sans-serif;
  background-color: rgb(54, 52, 51);
  color: #4d4d4d;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  padding-left: 150px;
}
input{
  font-family: inherit;
  font-size: 100%;
  line-height: 1.15;
  margin: 0;
  overflow: visible;
}
input[type="text"] {
  border-radius: 0;
}
#err{
  color: rgb(202, 9, 9);
  font-size: medium;
}
form{
  border: 4px solid black;
  background-color: rgb(85, 83, 83);
  align-items: center;
  padding-left: 25%;
  padding-top: 10%;
  width: 800px;
}
#submit{
  padding-left: 20%;
  padding-bottom: 20%;
  border-radius: 50%;
  height: 5px;
}
button{
  border-radius: 30%;
  height: 50px;
  width: 150px;
  background-color: slateblue;
}
h2{
  color:rgb(0, 0, 0);
}
@media screen and (min-width: 620px) {
  body {
    font-size: 1.9rem;
    line-height: 1.31579;
  }
}
  </style>
  