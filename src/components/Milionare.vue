
<template>
  <div class="milionare">
    <div class="grid-milionare flex-col flex">

      <div class="bg-blue-800 relative basis-1/4 row-up py-6">
        <figure class="flex h-full items-center justify-center">
          <img class="h-36" src="/public/Logo.png" alt="">
        </figure>
        <div>
          <span
            :class="Premio === 300 ? 'bg-amber-400 rounded-full absolute top-8 right-2 sm:right-12  px-6 py-2' : 'rounded-full absolute top-8 right-2 sm:right-12 bg-white px-6 py-2'">
            300
            <span v-if="Premio == 300">
              <i class="fa-solid text-amber-300 fa-star"></i>
            </span>
          </span>
          <span
            :class="Premio === 600 ? 'bg-amber-400 rounded-full absolute top-20 right-2 sm:right-12  px-6 py-2' : 'rounded-full absolute top-20 right-2 sm:right-12 bg-white px-6 py-2'">
            600
            <span v-if="Premio === 600">
              <i class="fa-solid text-amber-300 fa-star"></i>
            </span>
          </span>
          <span
            :class="Premio === 900 ? 'bg-amber-400 rounded-full absolute top-32 right-2 sm:right-12  px-6 py-2' : 'rounded-full absolute top-32 right-2 sm:right-12 bg-white px-6 py-2'">
            900
            <span v-if="Premio === 900">
              <i class="fa-solid text-amber-300 fa-star"></i>
            </span>
          </span>
          <span
            :class="Premio === 1200 ? 'bg-amber-400 rounded-full absolute top-44 right-2 sm:right-12  px-6 py-2' : 'rounded-full absolute top-44 right-2 sm:right-12 bg-white px-6 py-2'">
            1200
            <span v-if="Premio === 1200">
              <i class="fa-solid text-amber-300 fa-star"></i>
            </span>
          </span>
        </div>
      </div>
      <div v-if="Premio >= 0 && Premio <= 1100" class="bg-blue-950 basis-3/4 text-white row-down">
        <div v-for="( milio, index ) in  milionareRand " :key="milio.id" class="row-question relative pt-12">
          <img src="/public/punt-left.png" class="hidden sm:block left-question absolute" alt="">
          <span class="text-sm sm:text-base text-center border-2 rounded-md sm:border-x-0 sm:rounded-none 
            flex border-question border-solid py-4 px-4 mx-6 sm:m-0 sm:px-24  border-cyan-50  ">
            {{ milio.domanda }}
          </span>
          <img src="/public/punt-right.png" class="hidden sm:block right-question absolute" alt="">
        </div>

        <div v-for=" domanda  in  milionareRand " :key="domanda.id" class="answer grid-cols-1 sm:grid-cols-2 text-white">
          <div v-if="isRispostaCorreta === true" @click="RightOrNot" v-for=" risposte  in  domanda.risposte "
            :key="risposte.id" class="first-answer ps-10 relative">
            <!-- <img src="/public/punt-left.png" class="left-answer absolute" alt=""> -->
            <span class="border-answer border-solid py-2 px-5 border-cyan-50 border-2 ">
              {{ risposte }}
            </span>
            <!-- <img src="/public/punt-right.png" class="right-answer absolute" alt=""> -->
          </div>
          <div v-else>

            <button class="rounded bg-black px-3 py-2" @click="RandomElement">Ricomincia</button>

          </div>

          <!-- <div class="second-answer ps-10 relative">
              <img src="/public/punt-left.png" class="left-answer absolute" alt="">
              <span class="border-question border-solid py-2 px-5 border-cyan-50 border-2 ">
                B: {{ milio.risposte[1] }}
              </span>
              <img src="/public/punt-right.png" class="right-answer absolute" alt="">
            </div>

            <div class="third-answer ps-10 relative">
              <img src="/public/punt-left.png" class="left-answer absolute" alt="">
              <span class="border-question border-solid py-2 px-5 border-cyan-50 border-2 ">
                C: {{ milio.risposte[2] }}
              </span>
              <img src="/public/punt-right.png" class="right-answer absolute" alt="">
            </div>


            <div class="four-answer ps-10 relative">
              <img src="/public/punt-left.png" class="left-answer absolute" alt="">
              <span class="border-question border-solid py-2 px-5 border-cyan-50 border-2 ">
                D: {{ milio.risposte[3] }}
              </span>
              <img src="/public/punt-right.png" class="right-answer absolute" alt="">
            </div> -->
        </div>
        <!-- <button class="rounded bg-black px-3 py-2" v-if="isRispostaCorreta" @click="RandomElement">
          Prossimo
        </button> -->
      </div>
      <div class="bg-blue-950 basis-3/4 text-white row-down" v-else>

        <h1 class="text-yellow-400 text-5xl mt-16">HAI VINTOOO!!!!</h1>

        <button class="rounded bg-black px-3 py-2" @click="ReturnAnswer">Ricomincia</button>

      </div>
    </div>

  </div>
</template>


<script>
export default {
  props: ['id'],
  data() {
    return {

      milionare: [
        {
          "domanda": "Quale è la capitale della Francia?",
          "risposte": ["A: Roma", "B: Parigi", "C: Madrid", "D: Berlino"],
          "risposta_corretta": 1
        },
        {
          "domanda": "Chi scrisse il romanzo '1984'?",
          "risposte": ["A: George Orwell", "B: J.R.R. Tolkien", "C: F. Scott Fitzgerald", "D: Jane Austen"],
          "risposta_corretta": 0
        },
        {
          "domanda": "Qual è l'elemento chimico con simbolo Hg?",
          "risposte": ["A: Oro", "B: Mercurio", "C: Idrogeno", "D: Argento"],
          "risposta_corretta": 1
        },
        {
          "domanda": "In quale paese si trova la Grande Muraglia?",
          "risposte": ["A: Giappone", "B: Cina", "C: India", "D: Italia"],
          "risposta_corretta": 1
        },
        {
          "domanda": "Quale artista dipinse 'La Gioconda'?",
          "risposte": ["A: Leonardo da Vinci", "B: Pablo Picasso", "C: Vincent van Gogh", "D: Michelangelo"],
          "risposta_corretta": 0
        },
        {
          "domanda": "Qual è l'organo più grande del corpo umano?",
          "risposte": ["A: Cervello", "B: Cuore", "C: Fegato", "D: Pelle"],
          "risposta_corretta": 3
        },
        {
          "domanda": "Quale è il fiume più lungo del mondo?",
          "risposte": ["A: Nilo", "B: Mississippi", "C: Amazzonia", "D: Danubio"],
          "risposta_corretta": 0
        },
        {
          "domanda": "Chi è l'autore de 'I promessi sposi'?",
          "risposte": ["A: Giacomo Leopardi", "B: Alessandro Manzoni", "C: Dante Alighieri", "D: Italo Calvino"],
          "risposta_corretta": 1
        },
        {
          "domanda": "In quale città si trova il Colosseo?",
          "risposte": ["A: Parigi", "B: Atene", "C: Roma", "D: Barcellona"],
          "risposta_corretta": 2
        },
        {
          "domanda": "Quale è la lingua più parlata al mondo?",
          "risposte": ["A: Inglese", "B: Cinese mandarino", "C: Spagnolo", "D: Hindi"],
          "risposta_corretta": 1
        },
        {
          "domanda": "Quale pianeta del sistema solare è conosciuto come 'pianeta rosso'?",
          "risposte": ["A: Venere", "B: Marte", "C: Giove", "D: Saturno"],
          "risposta_corretta": 1
        },
        {
          "domanda": "Chi fu il primo uomo a camminare sulla Luna?",
          "risposte": ["A: Neil Armstrong", "B: Buzz Aldrin", "C: Yuri Gagarin", "D: John F. Kennedy"],
          "risposta_corretta": 0

        }
      ],
      milionareRand: [],
      isRispostaCorreta: true,
      Premio: 0,
    }
  },
  methods: {

    RandomElement() {
      const random = Math.floor(Math.random() * this.milionare.length)

      this.milionareRand.splice(0, 1)
      this.milionareRand.push(this.milionare[random])
      console.log(this.milionareRand)
      console.log(this.milionareRand[0].id)

    },
    RightOrNot() {
      console.log(this.milionareRand[0].risposta_corretta)
      console.log(this.milionare.length)
      console.log(this.milionareRand[0].risposte.indexOf(event.target.textContent))

      let ElementoCliccato = event.target.textContent
      const risposte = this.milionareRand[0].risposte

      const RispostaEsatta = this.milionareRand[0].risposta_corretta
      let indice = risposte.indexOf(ElementoCliccato)

      if (RispostaEsatta === indice) {
        this.isRispostaCorreta
        this.Premio += 100
        this.RandomElement()
      } else {
        this.Premio = 0
        this.isRispostaCorreta = false
        console.log('hai sbagliato')
      }


    },
    ReturnAnswer() {
      this.RandomElement()
      this.Premio = 0
    }
    // NextQuestion() {
    //   const indexCorrente = this.milionare.indexOf(this.milioCorrente);
    //   if (indexCorrente < this.milionare.length - 1) {
    //     this.milioCorrente = this.milionare[indexCorrente + 1];
    //   } else {
    //     // Se si raggiunge l'ultimo elemento, si può fare qualcosa come tornare al primo elemento
    //     this.milioCorrente = this.milionare[0];
    //   }
    //   console.log(this.$route)
    // }
  },
  mounted() {
    this.RandomElement()
    // Inizializza l'elemento corrente al primo elemento della lista quando il componente viene montato
    // this.milioCorrente = this.milionare[0];
  }
}
</script>



<style scoped>
.is-wrong {
  color: red;
}

.is-right {
  color: green;
}

.answer {
  display: grid;
  gap: 3rem;
}

.grid-milionare {
  height: 100vh;
  width: 100vw;
  overflow-x: hidden;
  overflow-y: auto;
}

.right-question {
  right: -27px;
  top: 48px;
  height: 56%;
}

.left-question {
  height: 56%;
  top: 48px;
  left: -29px;
}

.left-answer {
  top: -9px;
  left: 21px;
  height: 170%;
}

.right-answer {
  height: 170%;
  right: -8px;
  top: -9px;
}

.row-down {
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 71px;
}

.border-answer {
  border: 2px solid;
  border-radius: 10px;
}
</style>
