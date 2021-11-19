<template>
<img v-if="img" :src="img" alt="bg">
  <div class="bg-dark"></div> 
  <div class="indecision-container" >
  <h1>iT Is PosIbLe?</h1>
      <p>ONLY YES OR NO</p>
       <input v-model="question" tyoe="text" placeholder="Make a question here">
      <p>Remember! Allways finish with a question mark (?) </p>

      <div v-if="isValidQuestion" >
        <h3> {{question}} </h3>
        <h2> {{answer}} </h2>
      </div>
    </div>
</template>

<script>
export default {
    data(){
     return {
        question: null,
        answer: null,
        img: null
     }  
    },
    methods: {
        async getAnswer(){
            this.answer = "Thinking..."
            const {answer, image} = await fetch('https://yesno.wtf/api').then(r => r.json())
            this.img = image
            
            
            this.answer = ""
                
            
           }
    },
     watch:{
        question(value, oldValue){

            this.isValidQuestion = false

            if (!value.includes('?')) return

            this.isValidQuestion = true

            this.getAnswer();
        }
    }


}
</script>

<style scoped>

    img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 0px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }

</style>