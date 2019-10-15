<template>
  <div id="app">
    <div>
      <div class="button" v-for="item in this.alphabet">
          <button v-on:click="click(item.letter)"> {{ item.letter }} </button>
      </div>
    </div>
    Lettres utilisées :
    <div class="letter" v-for="item in lettreChoisi">
      {{ item }}
    </div>
    <div>
      <div class="letter" v-for="lettre in motRandom.toUpperCase()">
        <h1 v-if="lettreChoisi.includes(lettre)">{{ lettre }}</h1>
        <h1 v-else>_</h1>
      </div>
    </div>
    <br>
    <div>
      Nombre d'essais restants : {{ vies}}
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      vies: 10,
      total: 0,
      motRandom: '',
      wordList: [
        'bleu',
        'propagation',
        'citation',
        'facture',
        'annonce',
        'catastrophe',
      ],
      lettreChoisi: [],
      alphabet: [
        { letter: 'A' },
        { letter: 'B' },
        { letter: 'C' },
        { letter: 'D' },
        { letter: 'E' },
        { letter: 'F' },
        { letter: 'G' },
        { letter: 'H' },
        { letter: 'I' },
        { letter: 'J' },
        { letter: 'K' },
        { letter: 'L' },
        { letter: 'M' },
        { letter: 'N' },
        { letter: 'O' },
        { letter: 'P' },
        { letter: 'Q' },
        { letter: 'R' },
        { letter: 'S' },
        { letter: 'T' },
        { letter: 'U' },
        { letter: 'V' },
        { letter: 'W' },
        { letter: 'X' },
        { letter: 'Y' },
        { letter: 'Z' },
      ],
      bonneLettres: '',
    };
  },
  methods: {
    click(char) {
      // eslint-disable-next-line max-len
      if ((!(this.motRandom.toUpperCase().includes(char))) && !this.lettreChoisi.includes(char)) {
        this.vies -= 1;
        this.lettreChoisi.push(char);
        // eslint-disable-next-line max-len
      } else if (this.motRandom.toUpperCase().includes(char)) {
        this.lettreChoisi.push(char);
      }
      this.isWin();
    },
    isWin() {
      this.total = 0;
      this.motRandom.toUpperCase()
        .split('')
        .forEach((element) => {
          for (let i = 0; i <= this.lettreChoisi.length; i += 1) {
            if (this.lettreChoisi[i] === element) {
              this.total += 1;
            }
          }
        });
      if (this.total === this.motRandom.length) {
        alert('Vous avez gagné');
      }
      if (this.vies === 0) {
        alert('vous avez perdu');
        this.vies = 0;
      }
    },
  },

  created() {
    this.motRandom = this.wordList[Math.floor(Math.random() * this.wordList.length)];
  },
};
</script>

<style lang="scss">


.button {
  height: 2em;
  width: 2em;
  padding: 0.2em;
  display: inline-block;
}
.letter {
  height: 2em;
  width: 2em;
  padding: 0.2em;
  display: inline-block;
}
</style>
