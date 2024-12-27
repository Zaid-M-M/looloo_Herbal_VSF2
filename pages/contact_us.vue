<!-- Contact - USs -->

<template>
  <div class="ContactSec ">


    <div class="ContactMain ">
      <div class="content">
        <h1 class="reachUsHead">REACH US</h1>
  
      <!-- Content-->
        <div class="contentbox">
          <h3>Head Office</h3>
          <p>176/186 Hirji Korshi house, Null Bazaar, Mumbai – 400 003.</p>
        </div>
        <div class="contentbox">
          <h3>Sales Office</h3>
          <p>Mulji Jetha Cloth Market, Zaveri Bazaar, Mumbai – 400 002.</p>
        </div>
        <div class="contentbox">
          <h3>Customer Care</h3>
          <p><a href="tel:+919850817775">+91 98508 17775</a> </p>
        </div>
        <div class="contentbox">
          <h3>Email ID</h3>
          <p><a href="mailto:loolooherbal@gmail.com">loolooherbal@gmail.com</a> </p>
        </div>
      </div>
  
  
  
  
      <!-- From -->
      <div class="contactform">
        
        <div class="allInputCon">
          <h1 class="reachUsHead">WRITE US</h1>

          <form action="">
            <div class="inputCon">
              <label for="Full Name">Full Name *</label>
              <input type="text" name="Full Name" id="Full Name" required>
            </div>
  
            <div class="inputCon">
              <label for="Email">Email *</label>
              <input type="email" name="Email" id="Email" required>
            </div>
  
            <div class="inputCon">
              <label for="Phone">Phone *</label>
              <input type="number" name="Phone" id="Phone" required>
            </div>
  
            <div class="inputCon">
              <label for="Message">Message</label>
              <textarea  name="Message" id="Message" rows="6"  required> </textarea>
            </div>

            <button>Submit</button>

          </form>

        </div>
      </div>

    </div>

    
  </div>
</template>


<script>

export default({

  data() {
    return {
     
    };
  },
  methods: {
   
  },
});
</script>

<style scoped>
.y{border: 1px solid red}
.reachUsHead{
  margin: 10px 0px 20px 0px;
  font-size: 16px;
}
.contentbox{
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}



.contentbox p{
  margin: 0;
}


.ContactMain{
  max-width: 1300px;
  margin: 0 auto;
  padding: 70px 20px;
  gap: 20px;
}

.content h3{
  font-size: 15px;
  list-style: 20px;
}


.allInputCon form{
  display: flex;
  flex-direction: column;
  /* justify-content: space-between; */
  gap: 20px;
}

.inputCon{
  display: flex;  
  flex-direction: column;
}


.inputCon label{
  margin-bottom: 8px;
}
.inputCon input{
  padding: 8px;
}


.allInputCon form button{
  padding: 8px 15px;
  text-transform: uppercase;
  width: fit-content;
  background-color: #9f9f9f;
  border: none;
  outline: none;
  border-radius: 4px;
  font-size: 19px;
  color: #fff;
  font-weight: lighter;
  transition: all 0.3s ease-in-out;
  cursor: pointer;
}

.allInputCon form button:hover{
  background-color: green;
}


@media (min-width: 768px)  {
  .ContactMain{
    display: flex;
    padding: 70px 50px;
  }
  .content{
   flex: 1;
  }
  .contactform{
   flex: 1;
   
  }
}

@media (min-width: 1024px) {
  .ContactMain{
    padding: 70px 50px;
  }
}



</style>

