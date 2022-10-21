<script setup lang="ts">
import { onMounted, ref } from 'vue'

const props = withDefaults(
  defineProps<{
    startIndex?: number
    indexToStop: number
    delay?: number
  }>(),
  {
    startIndex: 0,
    indexToStop: 0,
    delay: 50,
  }
)
const counter = ref(props.startIndex)
const letters = [
  'A',
  'B',
  'C',
  'D',
  'E',
  'F',
  'G',
  'H',
  'I',
  'J',
  'K',
  'L',
  'M',
  'N',
  'O',
  'P',
  'Q',
  'R',
  'S',
  'T',
  'U',
  'V',
  'Z',
  '0',
  '1',
  '2',
  '3',
  '4',
  '5',
  '6',
  '7',
  '8',
  '9',
]
const letter1 = ref(letters[counter.value])
const letter2 = ref(letters[counter.value + 1])
const flipCardRef = ref()

function goForward() {
  counter.value = counter.value + 1
  letter1.value = letters[counter.value]
  letter2.value = letters[counter.value + 1] ?? letters[0]

  // Handle last letter
  if (!letters[counter.value + 1]) {
    counter.value = -1
  }
}

function handleTransitionEnd() {
  if (!flipCardRef.value) return

  flipCardRef.value.classList.remove('-hover')
  goForward()

  if (counter.value !== props.indexToStop) {
    setTimeout(init, 2)
  }
}

function init() {
  if (!flipCardRef.value) return
  flipCardRef.value.classList.add('-hover')
}

onMounted(() => {
  setTimeout(init, props.delay)
})
</script>

<template>
  <div class="flip-card" ref="flipCardRef" @transitionend="handleTransitionEnd">
    <div class="flip-card-top">
      <span>{{ letter2 }}</span>
    </div>
    <div class="flip-card-inner">
      <div class="flip-card-front">
        <span>{{ letter1 }}</span>
      </div>
      <div class="flip-card-back">
        <span>{{ letter2 }}</span>
      </div>
    </div>
    <div class="flip-card-bottom">
      <span>{{ letter1 }}</span>
    </div>
  </div>
</template>

<style scoped lang="scss">
.flip-card {
  background-color: transparent;
  width: 140px;
  height: 130px;
  perspective: 1000px;
}

.flip-card-inner {
  z-index: 1;
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transform-style: preserve-3d;
  transform-origin: 50% 100%;

  &:after {
    content: '';
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    height: 6px;
    background: black;
    transform: translateY(-50%);
  }
}

.flip-card.-hover .flip-card-inner {
  transform: rotateX(-180deg);
  transition: transform 0.2s;
}

.flip-card-front,
.flip-card-back,
.flip-card-top,
.flip-card-bottom {
  overflow: hidden;
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  background: #343333;

  span {
    position: absolute;
    top: 55%;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 120px;
    font-weight: bold;
    text-shadow: 0px 4px 4px black;
  }
}

.flip-card-front,
.flip-card-top {
  border-radius: 4px 4px 0 0;
  background: linear-gradient(to top, #232222, #343333);
}

.flip-card-back,
.flip-card-bottom {
  border-radius: 0 0 4px 4px;
  background: linear-gradient(to bottom, #232222 6%, #323232 20%, #232222 70%, #191919);
}

.flip-card-back {
  transform: rotateX(180deg);

  span {
    top: -45%;
  }
}

.flip-card-bottom {
  position: relative;

  span {
    top: -45%;
  }
}
</style>
