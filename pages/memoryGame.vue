<template>
  <div class="grid">
    <div
        v-for="(card, index) in cards"
        :key="index"
        :class="['card ', { 'flipped': card.flipped, 'matched': card.matched }]"
        @click="flipCard(index)"
    >
      <div class="front"></div>
      <div class="back">{{  card.value  }}</div>
    </div>
  </div>
  <button @click="resetGame">Reset</button>
</template>

<script>

export default {
  data() {
    return {
      cards: [
        { value: "A", flipped: false, matched: false },
        { value: "A", flipped: false, matched: false },
        { value: 'B', flipped: false, matched: false },
        { value: 'B', flipped: false, matched: false },
        { value: 'C', flipped: false, matched: false },
        { value: 'C', flipped: false, matched: false },
        { value: 'D', flipped: false, matched: false },
        { value: 'D', flipped: false, matched: false },
        { value: 'E', flipped: false, matched: false },
        { value: 'E', flipped: false, matched: false },
        { value: 'F', flipped: false, matched: false },
        { value: 'F', flipped: false, matched: false },
        { value: 'G', flipped: false, matched: false },
        { value: 'G', flipped: false, matched: false },
        { value: 'H', flipped: false, matched: false },
        { value: 'H', flipped: false, matched: false },
        { value: 'I', flipped: false, matched: false },
        { value: 'I', flipped: false, matched: false },
        { value: 'J', flipped: false, matched: false },
        { value: 'J', flipped: false, matched: false },
        { value: 'K', flipped: false, matched: false },
        { value: 'K', flipped: false, matched: false },
        { value: 'L', flipped: false, matched: false },
        { value: 'L', flipped: false, matched: false },
        { value: 'M', flipped: false, matched: false },
        { value: 'M', flipped: false, matched: false },
        { value: 'N', flipped: false, matched: false },
        { value: 'N', flipped: false, matched: false },
      ],
      flippedCards: [],
    };
  },
  methods: {
    flipCard(index) {
      const card = this.cards[index];

      if (!card.flipped && this.flippedCards.length < 2) {
        card.flipped = true;
        this.flippedCards.push(card);

        if (this.flippedCards.length === 2) {
          this.checkMatch();
        }
      }
    },
    checkMatch() {
      if (this.flippedCards[0].value === this.flippedCards[1].value) {
        this.flippedCards[0].matched = true;
        this.flippedCards[1].matched = true;
        this.flippedCards = [];
        this.checkWin();
      } else {
        setTimeout(() => {
          this.flippedCards[0].flipped = false;
          this.flippedCards[1].flipped = false;
          this.flippedCards = [];
        }, 1000);
      }
    },
    checkWin() {
      if (this.cards.every((card) => card.matched)) {
        alert('Congratulations! You won the game!');
      }
    },
    resetGame() {
      this.cards.forEach((card) => {
        card.flipped = false;
        card.matched = false;
      });
      this.flippedCards = [];
    },
    shuffleCards() {
      // Fisher-Yates shuffle algorithm
      for (let i = this.cards.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.cards[i], this.cards[j]] = [this.cards[j], this.cards[i]];
      }
    },
  },
  mounted() {
    this.shuffleCards(); // Shuffle cards when the component is mounted
  },
};
</script>

<style scoped>
.grid {
  display: flex;
  flex-wrap: wrap;
  max-width: 1200px;
  padding: 100px;
  margin: 0 auto;
}



.card {
  width: 120px;
  height: 120px;
  margin: 10px;
  border: 1px solid #000;
  cursor: pointer;
  perspective: 800px;
  transform-style: preserve-3d;
  transition: transform 0.5s;
}

.card.flipped {
  transform: rotateY(180deg);
}

.card.matched {
  background-color: #ccc;
  cursor: default;
}

.card > div {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
}

.card .front {
  background-image: url("../images/muster.jpg");

  width: 120px;
  height: 120px;
  margin-left: 0%;
  border: #2600ff 1px solid;
  box-shadow: 0 0 7px 2px ;}

.card .back {
  background-color: #fff;
  transform: rotateY(180deg);
  display: flex;
  align-items: center;
  justify-content: center;
}

button {
  display: block;
  margin: 10px auto;
}
</style>
