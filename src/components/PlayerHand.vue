<script setup>
import { ref } from 'vue';
import GameCard from './GameCard.vue';
import { usePlayerStore } from '@/stores/player';
import { storeToRefs } from 'pinia';

const playerStore = usePlayerStore();
const { hand } = storeToRefs(playerStore);

const cardIdRef = ref(0);
const isHandPanelVisible = ref(true);

const startingHandSize = 5;

const creatureCardList = [
  { name: "Applebug", power: 4, element: "Grass" },
  { name: "Babysnakes", power: 3, element: "Rock" },
  { name: "Bananakeet", power: 4, element: "Air" },
  { name: "Blobbyfish", power: 3, element: "Water" },
  { name: "Pippychicken", power: 2, element: "Air" },
  { name: "Pocketbat", power: 3, element: "Air" },
  { name: "Saladslug", power: 3, element: "Grass" },
  { name: "Squiddy", power: 4, element: "Water" },
  { name: "Stinkmink", power: 4, element: "Rock" },
  { name: "Turtlebunny", power: 5, element: "Grass" }
];

const equipmentCardList = [
  { name: "PetFood", effect: "Alter", value: 2 },
  { name: "RockCandy", effect: "Alter", value: 2 },
  { name: "YummyBones", effect: "Alter", value: 2 }
];

function drawCard() {
  const isCreatureCard = Math.random() >= 0.25;
  const cardData = generateRandomCard(isCreatureCard);
  const newCard = {};

  Object.assign(newCard, cardData);
  newCard.type = isCreatureCard ? "creature" : "equipment";
  newCard.id = cardIdRef.value++;
  hand.value.push(newCard);
}

for (let idx = 0; idx < startingHandSize; idx++) {
  drawCard();
}

function generateRandomCard(isCreatureCard) {
  const cardList = isCreatureCard ? creatureCardList : equipmentCardList;
  const randomIdx = Math.floor(Math.random() * cardList.length);
  return cardList[randomIdx];
}

function toggleHandPanel() {
  isHandPanelVisible.value = !isHandPanelVisible.value;
}

function playCard(id) {
  hand.value = hand.value.filter(card => card.id !== id);
}
</script>

<template>
  <div id="player-hand" v-show="isHandPanelVisible">
    <GameCard v-for="card in hand" :key="card.id" @click="playCard(card.id)" :name="card.name" :card-type="card.type"
      :power="card.power" />
  </div>
  <button class="btn btn--draw" @click="drawCard">Draw Card</button>
  <button class="btn btn--hide-hand" v-show="isHandPanelVisible" @click="toggleHandPanel">Hide Hand</button>
  <button class="btn btn--show-hand" v-show="!isHandPanelVisible" @click="toggleHandPanel">Show Hand</button>
</template>

<style scoped>
#player-hand {
  position: absolute;
  width: inherit;
  bottom: 10px;
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.btn {
  border: 2px solid #fff;
  margin: 5px;
  padding: 5px;
  position: absolute;
}

.btn--draw {
  bottom: 50px;
  left: 10px;
}

.btn--hide-hand,
.btn--show-hand {
  right: 10px;
  bottom: 10px;
}
</style>
