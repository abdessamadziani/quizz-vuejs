
<template>

  <main class="app">

   
    <div v-if="show" >
      <div style="text-align: center; color:#FFB84C; margin-top: 50px;">
    <h1 style="text-transform: uppercase;">AWS Academy</h1>
    <br><br>
    <h2 style="text-transform: uppercase;">show us your knowledge at our aws quizz</h2>
  </div>
      <div class="img">
        <img src="./assets/asset_logo_amazon-web-service.png" alt="img">
      </div>

  
<div class="division">
  
  <input
      class="name"
      type="text"
      name="name"
      id="name"
      v-model="name"
      placeholder="Enter your name"
    />
    <button type="submit" v-on:click="toggle" class="BtnGo">
      start
    </button>
</div>
    
   
  </div>
  <div v-else class="hole" >
    <h1 style="color:#FFB84C"> Welcome {{name}}</h1>
    <div class="container" id="container">
        <div class="child"  ref="bar"></div>
    </div>
    <section class="quiz" v-if=" !quizCompleted ">
      <div class="quiz-info">
       <span class="question">{{ getCurrentQuestion.question }}</span> 
       <br>
       <!-- <span class="score">{{score}}  / {{questions.length}}</span>  -->
      </div>

      <div class="options">
        <label
           v-for="(option,index) in getCurrentQuestion.options"
           :key="index"
           :class="`rlt-effect option ${
            getCurrentQuestion.selected == index 
            ? index == getCurrentQuestion.answer
            ? 'correct'
            :'wrong'
            : ''
           
           }
           ${
              getCurrentQuestion.selected != null && index != getCurrentQuestion.selected
              ? 'disabled'
              :''
            }
           `"
        >

          <input 
              type="radio"
              :name="getCurrentQuestion.index"
              :value="index"
              v-model="getCurrentQuestion.selected"
              :disabled="getCurrentQuestion.selected"
              @change="setAnswer"
 
          >
          <span>{{ option }}</span>


        </label>
      </div>
      <button class="BtnNext" @click="nextQuestion" ref="next">{{ getCurrentQuestion.index == questions.length - 1
      ? 'Finish'
      : getCurrentQuestion.selected == null 
         ? 'select an option'
         : 'Next Question' }}</button>
    </section>

    <section v-else>
      <div>
        <h2>Quizz Finished</h2>
        <h3> your score is {{ score }} / {{ questions.length }}</h3>
        <div>
          <ul>
            <li v-for="(question, index) in incorrect" :key="index">
              <!-- <p >{{ question.text }}</p> -->
              <p class="qst">The question : {{ question.question }}</p>
              <p class="crct">
                Correct answer : {{ question.options[question.answer] }}
              </p>
              <p class="your">
                Your answer : {{ question.options[question.selected] }}
              </p>
            </li>
          </ul>
        </div>

      </div>
    </section>
  </div>
  
  </main>

</template>


<script>
export default {
  data() {
    return {
      name: '',
      show:true,
    }
  },
  methods:
  {
    toggle() {
      if (this.name) {
        this.show = !this.show;
      } else if (!this.name) {
        this.inputError = "This field is required.";
      } else {
        this.inputError = "";
      }
    },
    sayhello:function(){
      return 'hello bro'
    },
    // nextQuestion: function () {
    //   this.$refs.bar.remove() 
    // },

    countDown: function (duration,q_count)
{
  // if(current_index<q_count)
  // {
  //    counter=setInterval(()=>{
  //     if(--duration<0)
  //     { 
  //       clearInterval(counter)
  //       this.$refs.next.click()
  //     }
  //   },1000)
  // }
  return duration + " "+ q_count
}



  }


}




</script>


<script setup>






import {ref,computed} from 'vue'








var incorrect=[];

const questions = ref([

    {
      question: 'what is vue js ?',
      answer: 0,
      options: [
        'a frontend freamwork',
        'a library',
        'an ice cream maker',
        'nothing'

      ],
      selected: null 

    },
    
    {
      question: 'what is html ?',
      answer: 1,
      options: [
        'a frontend freamwork',
        'hyper text markum language',
        'an ice cream maker',
        'nothing'

      ],
      selected: null 

    },
    
    {
      question: 'what is css  ?',
      answer: 2,
      options: [
        'a frontend freamwork',
        'a library',
        'cascading style sheet',
        'nothing'
      ],
      selected: null 

    },
    {
      question: 'what is bootstrap',
      answer: 0,
      options: [
        'a frontend freamwork of css',
        'a library',
        'cascading style sheet',
        'nothing'

      ],
      selected: null 

    }
     

])

const quizCompleted = ref(false)
const currentQuestion = ref(0)
  const score = computed(() => {
  let value = 0
  questions.value.map(q => {
     if(q.selected == q.answer)
        {
          value++;
        }
        else if (q.selected !== q.answer){
          incorrect.push(q)
          console.log(incorrect)
        }
  })
  return value
  })


const getCurrentQuestion = computed(() => {
    let question = questions.value[currentQuestion.value]
     question.index = currentQuestion.value
    return question
})

const setAnswer = evt => {
    questions.value[currentQuestion.value].selected = evt.target.value
    evt.target.value=null

}

const nextQuestion = () => {
  if(currentQuestion.value < questions.value.length -1)
     {
       currentQuestion.value++
     }
  else 
     {
      quizCompleted.value=true
     }   
}



</script>





<style>
*
{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
 body 
{
 background-color: #F5EAEA;
}
.img 
{
  width: 30%;
  margin: 50px auto;
}
.img img 
{
  width: 100%;
  border-radius:50%;

}
.name {
  /* border: 1px solid blue;
  color: black;
  padding: 10px;
  width: 140%;
  border-radius: 5px;
  background: #efeaf4; */
            display:block;
            width:400px;
            padding: 20px;
            font-size: 16px;
            font-weight: bold;
            border: none;
            border-top-left-radius: 10px;
            border-bottom-left-radius: 10px;
}
input:focus
         {
            padding-left:20px;
          
            outline-style: none;        

         }


 .BtnGo {
 
               width: 100%;
               padding: 20px 0;
               border: none;
               border-top-right-radius: 10px;
               border-bottom-right-radius: 10px;
               background-color:#ADA2FF;
               color: white;
               font-weight: bolder;
               font-size: 20px;
               cursor: pointer;

            
}

.division {
  position: fixed;
  top: 68%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
}
.hole 
{
  position: absolute;
  width: 80%;
  top: 50%;
  transform: translate( 0,-50%);
  border-radius: 10px;
  padding: 30px;
  background-color:#4D455D;

}

.app 
{
  width: 90%;
  margin:auto;
  padding: 20px;
  text-align: center;
  
}
.question 
{
  margin: 30px 0;
  display: block;
  width: 80%;
  background-color: black;
  color: white;
  margin: auto;
  padding: 30px 0;
  border-radius: 10px;
}
.options
{
  display: grid;
  grid-template-columns:  auto auto;
  gap: 15px;
   
}

 .options label  
{
  background-color:#EEEEEE;
  color: rgb(0, 0, 0);
  padding: 20px 30px;
  border-radius: 10px;
  cursor: pointer;

}
.options input 
{
  display: none;
}


.BtnNext
{
  display: block;
  margin: 40px auto;
  width: 40%;
  background: rgb(255,139,19);
  background: linear-gradient(214deg, rgba(255,139,19,1) 10%, rgba(0,0,0,1) 62%);
  border-radius: 10px;
  cursor: pointer;
  border: none;
  padding: 15px 25px;
  color: white;
} 



.rlt-effect
{
  position: relative;
}
.rlt-effect::before
{
  position:absolute;
  content: "";
  top:0;
  left: 0;
  right: 0;
  bottom: 0;
  width:0;
  /* z-index:10; */
  border-radius:10px ;
  transition: width 0.5s;
  background-color:#FFB84C;

}
.rlt-effect:hover::before
{
  width: 100%;
}

 label.correct{
  background-color: rgb(101, 239, 101);
}
label.wrong{
  background-color: rgb(235, 98, 126);
}




.rlt-effect:hover span
{
   color: rgb(255, 255, 255);
   position: relative;
   transition: color 0.5s;

}


.container
{
   width: 100%;
   height:30px;
   margin: 20px 0;
   position: relative;
   background-color: rgb(255, 255, 255);
   border-top-right-radius: 15px;
   border-bottom-right-radius: 15px;


}
.child
   {
      position: absolute;
      background-color: rgb(166, 30, 235);
      height: 100%;
      width: 50%;
      border-top-right-radius: 15px;
      border-bottom-right-radius: 15px;
      animation: bardown 30s forwards;

   }


   .qst 
   {
     display: block;
     widows: 80%;
     padding: 15px;
     background-color: #ea5a4d;
     color: white;

   }
   .crct 
   {
     display: block;
     widows: 80%;
     padding: 15px;
     background-color: #25dc81;
     color: white;

   }
   .your 
   {
    display: block;
     widows: 80%;
     padding: 15px;
     background-color: #000000;
     color: white;
   }

   @keyframes bardown
{
   0%
   {
      width: 100%;
   }
   100%
   {
      width: 0%;
   }

}
</style>
