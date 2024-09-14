<script setup>
import { ref } from 'vue';
import GameCard from './GameCard.vue';

const cardIdRef = ref(6);
const isHandPanelVisible = ref(true);

const creatureCardNames = ["AppleBug", "Babysnakes", "Bananakeet", "Blobbyfish", "PippyChicken", "PocketBat", "SaladSlug", "Squiddy", "StinkMink", "TurtleBunny"];
const equipmentCardNames = ["PetFood", "RockCandy", "YummyBones"];

const playerHand = ref([
  { petName: "Bananakeet", type: "creature", id: 1 },
  { petName: "Babysnakes", type: "creature", id: 2 },
  { petName: "RockCandy", type: "equipment", id: 3 },
  { petName: "PocketBat", type: "creature", id: 4 },
  { petName: "TurtleBunny", type: "creature", id: 5 }
]);

function drawCard() {
  const isCreatureCard = Math.random() >= 0.25;
  const cardName = generateRandomCard(isCreatureCard);
  const newCard = {};

  if (isCreatureCard) {
    newCard.petName = cardName;
    newCard.type = "creature";
  } else {
    newCard.toolName = cardName;
    newCard.type = "equipment";
  }

  newCard.id = cardIdRef.value++;
  playerHand.value.push(newCard);
}

function generateRandomCard(isCreatureCard) {
  const cardList = isCreatureCard ? creatureCardNames : equipmentCardNames;
  const randomIdx = Math.floor(Math.random() * cardList.length);
  return cardList[randomIdx];
}

function toggleHandPanel() {
  isHandPanelVisible.value = !isHandPanelVisible.value;
}

function playCard(id) {
  playerHand.value = playerHand.value.filter(card => card.id !== id);
}
</script>

<template>
  <div id="player-hand" v-show="isHandPanelVisible">
    <GameCard v-for="card in playerHand" :key="card.id" @click="playCard(card.id)" :pet-name="card.petName"
      :tool-name="card.toolName" :card-type="card.type" />
  </div>
  <button class="btn btn--draw" @click="drawCard">Draw Card</button>
  <button class="btn btn--hide-hand" v-show="isHandPanelVisible" @click="toggleHandPanel">Hide Hand</button>
  <button class="btn btn--show-hand" v-show="!isHandPanelVisible" @click="toggleHandPanel">Show Hand</button>
</template>

<style scoped>
#player-hand {
  position: absolute;
  text-align: center;
  width: inherit;
  bottom: 10px;
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
