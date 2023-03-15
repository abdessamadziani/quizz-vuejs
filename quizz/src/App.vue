
<template>

  <main class="app">

   
    <div v-if="show" >
      <div style="text-align: center; color:#FFB84C; margin-top: 50px;">
    <h1 style="text-transform: uppercase; font-size:55px;">AWS <span style="color:white;text-transform: capitalize;">Cloud  </span>Academy</h1>
    <br><br>
    <h2 style="text-transform:capitalize;">show us your knowledge at our aws cloud quizz enjoy it</h2>
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
    <!-- <div class="container" id="container">
        <div class="child"  ref="bar"></div>
    </div> -->
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
      <div class="btn-cercle">
      <button class="BtnNext" @click="nextQuestion" ref="next">{{ getCurrentQuestion.index == questions.length - 1
      ? 'Finish'
      : getCurrentQuestion.selected == null 
         ? 'Select An Option'
         : 'Next Question' }}</button>


       <div class="cercle">
        <span>{{currentQuestion +1 }} / {{ questions.length }}</span>
       </div>


</div>
    </section>

    <section v-else>
      <div class="res-area">
        <h1 style="color:white;font-size:40px;">Quizz Finished</h1>
        <h2 class="score" > your score is {{ score }} / {{ questions.length }}</h2>
        <div style="margin-top: 25px;">
          <ul>
            <li v-for="(question, index) in incorrect" :key="index">
              <!-- <p >{{ question.text }}</p> -->
              <p class="qst">The question : {{ question.question }}</p>
              <p class="crct">
                Correct answer : {{ question.options[question.answer] }}
              </p>
              <p style="margin-bottom: 20px;" class="your">
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
      question: 'Why is AWS more economical than traditional data centers for applications with varying computeworkloads?',
      answer: 2,
      options: [
        'Amazon EC2 costs are billed on a monthly basis',
        'Users retain full administrative access to their Amazon EC2 instances',
        'Amazon EC2 instances can be launched on demand when needed',
        'Users can permanently run enough instances to handle peak workloads'

      ],
      selected: null 

    },
    
    {
      question: 'Which AWS service would simplify the migration of a database to AWS?',
      answer: 1,
      options: [
        'AWS Storage Gateway',
        'AWS Database Migration Service (AWS DMS)',
        'Amazon EC2',
        'Amazon AppStream 2.0'

      ],
      selected: null 

    },
    
    {
      question: 'Which AWS offering enables users to find, buy, and immediately start using software solutions in their AWS environment?',
      answer: 3,
      options: [
        'AWS Config',
        'AWS OpsWorks',
        'AWS SDK',
        'AWS Marketplace'
      ],
      selected: null 

    },
    {
      question: 'Which AWS networking service enables a company to create a virtual network within AWS?',
      answer: 3,
      options: [
        'AWS Config',
        'Amazon Route 53',
        'AWS Direct Connect',
        'Amazon Virtual Private Cloud (Amazon VPC)'

      ],
      selected: null 

    },

    
    {
      question: 'Which of the following is an AWS responsibility under the AWS shared responsibility model?',
      answer: 1,
      options: [
        'Configuring third-party applications',
        'Maintaining physical hardware',
        'Securing application access and data',
        'Managing guest operating systems'

      ],
      selected: null 

    },
    {
      question: 'Which component of the AWS global infrastructure does Amazon CloudFront use to ensure low-latency delivery?',
      answer: 1,
      options: [
        'AWS Regions',
        'Edge locations',
        'Availability Zones',
        'Virtual Private Cloud (VPC)'

      ],
      selected: null 

    },
    {
      question: 'How would a system administrator add an additional layer of login security to a user\'s AWS Management Console?',
      answer: 3,
      options: [
        'se Amazon Cloud Directory',
        'Audit AWS Identity and Access Management (IAM) roles',
        'Enable multi-factor authentication',
        'Enable AWS CloudTrail'

      ],
      selected: null 

    },
    {
      question: 'Which service can identify the user that made the API call when an Amazon EC2 instance is terminated?',
      answer: 1,
      options: [
        'AWS Trusted Advisor',
        'AWS CloudTrail',
        'AWS X-Ray',
        'AWS Identity and Access Management (AWS IAM)'

      ],
      selected: null 

    },
    {
      question: 'Which service would be used to send alerts based on Amazon CloudWatch alarms?',
      answer: 0,
      options: [
        'Amazon Simple Notification Service (Amazon SNS)',
        'AWS CloudTrail',
        'AWS Trusted Advisor',
        'Amazon Route 53'

      ],
      selected: null 

    },
    {
      question: 'Where can a user find information about prohibited actions on the AWS infrastructure?',
      answer: 3,
      options: [
        'AWS Trusted Advisor',
        'AWS Identity and Access Management (IAM)',
        'AWS Billing Console',
        'AWS Acceptable Use Policy'

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
@import url('https://fonts.googleapis.com/css2?family=Clicker+Script&family=Pacifico&family=Permanent+Marker&family=Poppins:ital,wght@0,200;0,300;0,400;1,400;1,500&family=Rubik+Gemstones&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Clicker+Script&family=Montserrat:ital,wght@0,100;0,500;0,600;0,700;1,600&family=Pacifico&family=Permanent+Marker&family=Rubik+Gemstones&display=swap');
*
{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
 body 
{
 background-color: #F5EAEA;
font-family: 'Montserrat', sans-serif;
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
            width:500px;
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
.btn-cercle 
{
  display: flex;
  justify-content:space-evenly;


}

.cercle 
{
  position: relative;
  border:10px solid white;
  width:200px;
  border-radius: 50%;
  margin: 50px 0;
  padding: 30px;

}
.cercle span
{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 20px;
}

.app 
{
  width: 90%;
  margin:auto;
  padding: 20px;
  text-align: center;
  
}
.quiz-info 
{
  margin: 30px 0;
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
  padding: 30px 35px;
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
  margin: 40px 70px;
  width: 35%;
  background: rgb(255,139,19);
  background: linear-gradient(214deg, rgba(255,139,19,1) 10%, rgba(0,0,0,1) 62%);
  border-radius: 10px;
  cursor: pointer;
  border: none;
  padding: 20px 30px;
  color: white;
  font-size: 30px;
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
     background-color: #a18888;
     color: white;
     margin-bottom: 20px;
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

.res-area 
{
  background-color: rgb(0, 0, 0);
   width: 80%;
   max-height: 70vh;
   overflow: auto;
   border: 10px solid grey;
   margin: 10px auto;
   text-align: center;
   line-height: 1.9;
   padding: 10px;
}
.score 
{
  color: white;
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  width: 50%;
  padding: 15px 24px;
  background-color: #25dc81;
  margin: 30px auto;

}
</style>
