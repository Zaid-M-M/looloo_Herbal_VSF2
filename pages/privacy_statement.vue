<!-- Privacy - Statement -->

<template>
  <div class="PrivacyMainSec">
    <div class="accordion-item PrivacyAccorMain" v-for="(item, index) in accordionData" :key="index">
      <div class="accordion-header" @click="toggleAccordion(index)">
        <span class="icon">
          <img v-if="isActive(index)" src="../static/add.svg" />
          <img v-else src="../static/minus.svg" />
        </span>
        <button class="accordion-title">{{ item.title }}</button>
      </div>
      <transition
        @before-enter="beforeEnter"
        @enter="enter"
        @leave="leave"
      >
        <div v-show="isActive(index)" class="accordion-content">
          <!-- <p class="accorPara">{{ item.content }}</p> -->
          <p class="accorPara" v-html="item.content"></p>
        </div>
      </transition>
    </div>
  </div>
</template>


<script>


export default({
  data() {
    return {
      activeIndex: null, 
      accordionData: [

        { title: "Section 1 - what do we do with your information?", content: `<p>
          When you purchase something from our store, as part of the buying and selling process, we collect the personal information you give us such as your name, address and email address.When you browse our store, we also automatically receive your computer’s internet protocol (IP) address in order to provide us with information that helps us learn about your browser and operating system. Email marketing (if applicable): With your permission, we may send you emails about our store, new products and other updates.
          </p>` },
        { title: "Section 2 - consent", content: ` <strong>How do you get my consent?</strong> 
        <p>When you provide us with personal information to complete a transaction, verify your credit card, place an order, arrange for a delivery or return a purchase, we imply that you consent to our collecting it and using it for that specific reason only. If we ask for your personal information for a secondary reason, like marketing, we will either ask you directly for your expressed consent, or provide you with an opportunity to say no . </br>
        If we ask for your personal information for a secondary reason, like marketing, we will either ask you directly for your expressed consent, or provide you with an opportunity to say no.</p> 
        <strong>How do I withdraw my consent?</strong>
        <p>
          If after you opt-in, you change your mind, you may withdraw your consent for us to contact you, for the continued collection, use or disclosure of your information, at anytime, by contacting us at shandhamankar@gmail.com or mailing us at: Looloo Herbal 1st Floor, Null Bazaar, Mumbai, MH, 400003, India.  
        </p>` },
        { title: "Section 3 - disclosure", content: `<p>
         We may disclose your personal information if we are required by law to do so or if you violate our Terms of Service.
        </p>` 
      },
      { title: "Section 4 - third-party services", content: `<p>
        In general, the third-party providers used by us will only collect, use and disclose your information to the extent necessary to allow them to perform the services they provide to us.  <br />  <br />
        However, certain third-party service providers, such as payment gateways and other payment transaction processors, have their own privacy policies in respect to the information we are required to provide to them for your purchase-related transactions. <br />
        For these providers, we recommend that you read their privacy policies so you can understand the manner in which your personal information will be handled by these providers. <br />  <br />
        In particular, remember that certain providers may be located in or have facilities that are located in a different jurisdiction than either you or us. So if you elect to proceed with a transaction that involves the services of a third-party service provider, then your information may become subject to the laws of the jurisdiction(s) in which that service provider or its facilities are located. < /br>  <br />
        As an example, if you are located in Canada and your transaction is processed by a payment gateway located in the United States, then your personal information used in completing that transaction may be subject to disclosure under United States legislation, including the Patriot Act. <br />  <br />
        Once you leave our store’s website or are redirected to a third-party website or application, you are no longer governed by this Privacy Policy or our website’s Terms of Service.<br />  <br />
        When you click on links on our store, they may direct you away from our site. We are not responsible for the privacy practices of other sites and encourage you to read their privacy statements.<br />  

        </p>` },
      { title: "Section 5 - security",
       content: `<p>
            To protect your personal information, we take reasonable precautions and follow industry best practices to make sure it is not      inappropriately lost, misused, accessed, disclosed, altered or destroyed.
        </p>
        <p>
          If you provide us with your credit card information, the information is encrypted using secure socket layer technology (SSL) and stored with a AES-256 encryption. Although no method of transmission over the Internet or electronic storage is 100% secure, we follow all PCI-DSS requirements and implement additional generally accepted industry standards.
        </p>`
    
    
    },
      { title: "Section 6 - age of consent", content: `<p>
      By using this site, you represent that you are at least the age of majority in your state or province of residence, or that you are the age of majority in your state or province of residence and you have given us your consent to allow any of your minor dependents to use this site.
      </p>` },
      { title: "Section 7 - changes to this privacy policy", content: `<p>
      We reserve the right to modify this privacy policy at any time, so please review it frequently. Changes and clarifications will take effect immediately upon their posting on the website. If we make material changes to this policy, we will notify you here that it has been updated, so that you are aware of what information we collect, how we use it, and under what circumstances, if any, we use and/or disclose it.</p>
      <p>If our store is acquired or merged with another company, your information may be transferred to the new owners so that we may continue to sell products to you.</p>
      
      ` },
      { title: "Questions and contact information", content: `<p>If you would like to: access, correct, amend or delete any personal information we have about you, register a complaint, or simply want more information contact our Privacy Compliance Officer at loolooherbal@gmail.com or by mail at Looloo Herbal.</p>

      <p>[Re: Privacy Compliance Officer]</p>
      <p>[1st Floor, Null Bazaar, Mumbai, MH, 400003, India]</p>
      
      ` },
      
        
        
      ],
    };
  },
  methods: {
    toggleAccordion(index) {
      this.activeIndex = this.activeIndex === index ? null : index;
    },
    isActive(index) {
      return this.activeIndex === index;
    },
    beforeEnter(el) {
      el.style.height = '0';
    },
    enter(el) {
      el.style.height = el.scrollHeight + 'px';
    },
    leave(el) {
      el.style.height = el.scrollHeight + 'px';
      setTimeout(() => {
        el.style.height = '0';
      });
    }
  },
});
</script>

<style scoped>
.b{border: 1px solid red;}
.accordion-content {
  overflow: hidden;

}

/* Transition for smooth height change */
.accordion-enter-active, .accordion-leave-active {
  transition: all 0.4s ease;
}

/* .accordion-enter, .accordion-leave-to {
  height: 0;
} */
.PrivacyMainSec{
  background-color: #f5f1dd;
  padding: 70px 0px 70px 0px;
}
.PrivacyAccorMain{
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 50px;
}

.accordion-header{
  background-color: #f9f9f9;
  padding: 5px 20px;
  display: flex;
  align-items: center;
  cursor: pointer;
 




  .icon{
    font-size: 18px;
    width: 40px;
  }


}


.accordion-item {
  margin-bottom: 10px;
}

.accordion-title {
  background-color: transparent;
  cursor: pointer;
  padding: 10px;
  border: none;
  text-align: left;
  outline: none;
  /* transition: background-color 0.3s; */
  font-size: 20px;
  line-height: 20px;
  color: #666;
}




.accordion-header:hover {
  background-color: #f0f0f0;
}

.accordion-content {
  padding: 10px;
  border-top: none;
  margin: 10px 0px;
  background-image: linear-gradient(to bottom, rgba(255, 255, 255, .2) 0, rgba(255, 255, 255, .01) 100%);
  background-repeat: repeat-x;
  border-width: 1px;
  font-size: 18px;
  line-height: 25px;
  color: #6d6b5d;
  transform: translate3d(0, 0, 0);
  transition: all 0.5s ease-in-out;
  display: block !important;
  height: 0;
}

@media (max-width: 768px) {
  .PrivacyMainSec{
    padding: 30px 0px 30px 0px;
  }
  .PrivacyAccorMain{
   width: 90%;
   margin: 0 auto;
   padding: 0;
  }
  .accordion-title{
    font-size: 17px;
  }
}
@media (min-width:768px) and (max-width: 1024px) {
  .PrivacyAccorMain{
   width: 90%;
   margin: 0 auto;
  }
  .accordion-title{
    font-size: 17px;
  }
}

/* @media (min-width:1367px) {

} */
</style>

