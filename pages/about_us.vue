about us page
<template>
  <div>
    <div class="aboutMain">
      <div class="broderDiv">
  
        <div class="contentDiv">
          <p>Khojati, a Unani Institution established in 1847, has a reputation of producing potent Eye Care Products. A hundred and fifty years back, a unique formula for a Surma was handed over to Bai Ratanbai Manji Padamshi Surmawalla. It involved the use of genuine pearls and effective ancient herbs. This marked the beginning of Khojati while leaving its founders with a vision to provide pure herbal remedies for generations to come. The brand gained positive reputation and kept growing right from when it was set up; it became a brand loved, shared, and trusted across the globe.</p>
          <p>Khojati, by the virtue of being ambitious and creative, responsibly expanded its vision beyond the realm of eye care. LooLoo, founded by Mr. Amin Usman Banatwalla, fulfilled this agenda in 1995 by launching a wide range of herbal products that are devoid of any harmful side effects and animal derivatives. Accordingly, Looloo products are highly effective and 100% vegetarian.</p>
          <p>The R&D department at LooLoo is highly responsible and takes utmost care in developing its wide range of herbal products. A substantial amount of time and effort is invested in making sure that the resulting products are capable of curing the troubles rather than merely subsiding them.</p>
        </div>
      
     </div>

    </div>

   
  </div>


</template>

<script>
export default ({

  
});

</script>

<style scoped>
* {
  box-sizing: border-box;
}

body {
  font-family: Verdana, sans-serif;
  margin: 0;
}


.aboutMain{
  padding-top: 120px;
  padding-bottom: 80px;
  display: flex;
  justify-content: center;
}


.broderDiv{
  background-color: #fffdf0;
  border: 13px solid #05923f;
  font-size: 17px;
  font-family: 'Oxygen', sans-serif;
  font-weight: 400;
  color: #000;
  letter-spacing: 0.5px;
  line-height: 29px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  max-width: 700px;

}

.contentDiv {
  padding: 30px 30px;
  max-width: 600px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  outline: 2px solid #d2b930;
}


@media (max-width: 768px) {
  .broderDiv{
    width: 90%;
    padding: 19px 19px;
  }

  .contentDiv{
    padding: 15px 20px;
    
  }
}

</style>
