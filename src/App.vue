<template>
  <div id="app">

      <div class="navigation">
        <h1>Sprawdź swoją wiedzę!</h1>
      </div>

      <div class="info">
        <Informations :gamer="gamer" />
      </div>

      <div class="question">
        <Question :textQuestion="Questions[game].question" /> 
      </div>

      <div class="answer answer-1">
          <Answer :textAnswer="Questions[game].answers[0]" 
                  @selectAnswer="updateData($event)"/>
      </div>

      <div class="answer answer-2">
          <Answer :textAnswer="Questions[game].answers[1]" 
                  @selectAnswer="updateData($event)"/>
      </div>

      <div class="answer answer-3">
          <Answer :textAnswer="Questions[game].answers[2]" 
                  @selectAnswer="updateData($event)"/>
      </div>

      <div class="answer answer-4">
          <Answer :textAnswer="Questions[game].answers[3]" 
                  @selectAnswer="updateData($event)"/> 
      </div>

      <div class="endGame">
        <button class="endGame__button" @click="this.endGame">Koniec gry</button>
      </div>

      <div class="footer">
        <p>Projekt i implementacja: <a class="footer__a" href="http://www.buttermilk.pl/">Mariusz Maślanka</a>
          <br />
           Odwiedź moją stronę <a class="footer__a" href="http://www.buttermilk.pl/">Buttermilk</a>
        </p>
      </div>
    
  </div>
</template>

<script>

import Question from './components/Question.vue';
import Informations from './components/Informations.vue';
import Answer from './components/Answer.vue';
import { setTimeout } from 'timers';

export default {
  name: 'App',

  data() {
    return{
      
      game: 0,
      gamer: {
        score: 0,
        opportunities: 3,
        
      },

      Questions: [
        {idQuestion: 1, question: "Kto jest mistrzem Polski w hokeju na lodzie?", answers: [
          {idAnsewer: 1, answer: "Comarch Cracovia", truth: false},
          {idAnsewer: 2, answer: "GKS Tychy", truth: true},
          {idAnsewer: 3, answer: "TatrySki Podhale Nowy Targ", truth: false},
          {idAnsewer: 4, answer: "Tauron KH GKS Katowice", truth: false},
          ],
        },
        {idQuestion: 2, question: "Które miasto jest stolicą Niemiec?", answers: [
          {idAnsewer: 1, answer: "Hamburg", truth: false},
          {idAnsewer: 2, answer: "Frankfurt", truth: false},
          {idAnsewer: 3, answer: "Stuttgart", truth: false},
          {idAnsewer: 4, answer: "Berlin", truth: true},
          ],
        },
        {idQuestion: 3, question: "Która z poniższych osób nie była prezydentem Polski?", answers: [
          {idAnsewer: 1, answer: "Lech Kaczyński", truth: false},
          {idAnsewer: 2, answer: "Donald Tusk", truth: true},
          {idAnsewer: 3, answer: "Bronisław Komorowski", truth: false},
          {idAnsewer: 4, answer: "Lech Wałęsa", truth: false},
          ],
        },
        {idQuestion: 4, question: "Jaki jest najstarszy klub piłkarski w Polsce?", answers: [
          {idAnsewer: 1, answer: "Wisła Kraków", truth: false},
          {idAnsewer: 2, answer: "Legia Warszawa", truth: false},
          {idAnsewer: 3, answer: "Górnik Zabrze", truth: false},
          {idAnsewer: 4, answer: "Cracovia", truth: true},
          ],
        },
        {idQuestion: 5, question: "Wskaż datę zakończenia I wojny światowej...", answers: [
          {idAnsewer: 1, answer: "11 listopada 1918", truth: true},
          {idAnsewer: 2, answer: "10 listopada 1918", truth: false},
          {idAnsewer: 3, answer: "11 listopada 1917", truth: false},
          {idAnsewer: 4, answer: "11 listopada 1919", truth: false},
          ],
        },
      ],
    };
  },

  components: {
    Question,
    Informations,
    Answer,
  },

  methods:{

    endGame(){
      
      alert("Zdobyłeś: " + this.gamer.score + " punktów");
      this.gamer.score = 0;
      this.gamer.opportunities = 3;
      this.game = 0;
    },

    endGameDetails(){
      console.log("Twój wynik to: " + this.gamer.score + " punktów");
    },

    updateData(updatedObject){
      setTimeout(() => {
        this.gamer.score += updatedObject.score;
        this.gamer.opportunities += updatedObject.opportunities;
        //this.game = this.randomQuestion();
        this.game++;
        
        if(this.game >= this.Questions.length){
          alert("Przepraszamy ale nie mamy więcej pytań - dodamy je wkrótce ;)");
          this.endGameDetails();
          this.endGame();
        }
      }, 500)
    },

    initializeIndexQuestionTab(){

      
    },
    
    // randomQuestion(){

    //   var randomNumber = Math.floor(Math.random()*this.Questions.length);

    //   for(let i = 0; i < this.indexQuestion.length(); i++){

    //       while(randomNumber == this.indexQuestion[i]){
    //         randomNumber = Math.floor(Math.random()*this.Questions.length);
    //       }

    //   }

    //   return randomNumber;
    
    // },
  },
}
</script>

<style>

#app{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  display: grid;
  width: 100vw;
  height: 100vh;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows: repeat(12, 1fr);
 /* background-color: aliceblue; */
 background-color: rgba(0, 194, 224, 1);
  opacity: 0.1 blue;
  -webkit-filter: saturate(150%);
  -moz-filter: saturate(150%);
  -o-filter: saturate(150%);
  -ms-filter: saturate(150%);
  filter: saturate(150%);
}

.navigation{
  text-align: center;
  grid-column: 1/ 9;
  grid-row: 1/ 3;
  background-color: rgba(0, 194, 224, 1);
  opacity: 0.8;
}

.info{
  grid-column: 6/ 9;
  grid-row: 3/ 5;
   background-color: rgba(0, 194, 224, 1);
  opacity: 0.8;
  text-align: center;
}

.question{
  grid-column: 2/ 8;
  grid-row:   5/ 8;
  background-color: rgba(0, 194, 224, 1);
  opacity: 0.8;
  text-align: center;
}

.answer{
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  background-color: #FFFF99;
  text-align: center;
  cursor: pointer;
  font-size: 1.5em;
  border-left: 2px solid blue;
}

.answer:hover{

  transition: 0.4s;
  background-color: #eeff00;
  font-size: 2em;
  border-left: 20px solid blue;
  
}
.answer-1{
  grid-column: 1/ 3;
  grid-row:   8/ 10;
}

.answer-2{
  grid-column: 3/ 5;
  grid-row:   8/ 10;
}

.answer-3{
  grid-column: 5/ 7;
  grid-row:   8/ 10;
}

.answer-4{
  grid-column: 7/ 9;
  grid-row:   8/ 10;
}

.endGame{
  grid-column: 4/ 6;
  grid-row:   10/ 12;
  text-align: center;
  padding-top: 10px;
  
}

.endGame__button{
  width: 75%;
  height: 50%;
  border: none;
  background-color: rgba(255, 0, 0, 0.7);
  opacity: 0.9;
  font-size: 1.5em;
  font-weight: bold;
}

.endGame__button:hover{
  
  background-color: rgba(255, 0, 0, 1);
  transition: 0.5s;

}

.footer{
  grid-column: 1/ 9;
  grid-row:   12/ 13;
  text-align: center;
  background-color: rgba(0, 194, 224, 1);
  opacity: 0.8;
  
}

.footer__a {
  text-decoration: none;
  color: black;
  font-weight: bold;
}


</style>
