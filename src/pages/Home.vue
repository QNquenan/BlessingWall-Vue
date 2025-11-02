<template>
    <div class="home-container">
        <motion.div v-for="card in cards" :key="card.id" :initial="{ opacity: 0, scale: 0 }"
            :animate="{ opacity: 1, scale: 1 }" :exit="{ opacity: 0, scale: 0 }" :transition="{ duration: 0.3 }" :style="{
                position: 'absolute',
                left: card.left + 'px',
                top: card.top + 'px'
            }">
            <WindowsCard :body-content="card.content" :body-bg-color="card.bodyColor" :style="{
                transform: `rotate(${card.rotation}deg)`
            }" />
        </motion.div>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { motion } from "motion-v";
import WindowsCard from '../components/WindowsCard.vue';
import blessing from '../assets/config/Blessing.json';

const blessList = blessing;
const cards = ref([]);

let intervalId = null;
let cardIdCounter = 0;

// 生成随机颜色
const generateRandomColor = () => {
    let r, g, b;

    const highValue = 200 + Math.floor(Math.random() * 56);
    const minValue = 100 + Math.floor(Math.random() * 156);
    const highChannel = Math.floor(Math.random() * 3);

    if (highChannel === 0) {
        r = highValue;
        g = minValue;
        b = 100 + Math.floor(Math.random() * 156);
    } else if (highChannel === 1) {
        r = 100 + Math.floor(Math.random() * 156);
        g = highValue;
        b = minValue;
    } else {
        r = minValue;
        g = 100 + Math.floor(Math.random() * 156);
        b = highValue;
    }

    r = Math.max(r, 100);
    g = Math.max(g, 100);
    b = Math.max(b, 100);

    return `rgb(${r}, ${g}, ${b})`;
};

// 创建新卡片
const createRandomCard = () => {
    const windowWidth = window.innerWidth;
    const windowHeight = window.innerHeight;

    const cardWidth = 200;
    const cardHeight = 150;

    const left = Math.random() * (windowWidth - cardWidth);
    const top = Math.random() * (windowHeight - cardHeight);

    const rotation = Math.random() > 0.3 ?
        -(3 + Math.random() * 3) :
        (3 + Math.random() * 3);

    const bodyColor = generateRandomColor();

    const content = blessList[Math.floor(Math.random() * blessList.length)];

    return {
        id: cardIdCounter++,
        content,
        bodyColor,
        left,
        top,
        rotation
    };
};

onMounted(() => {
    for (let i = 0; i < 5; i++) {
        cards.value.push(createRandomCard());
    }

    intervalId = setInterval(() => {
        cards.value.push(createRandomCard());

        if (cards.value.length > 100) {
            cards.value.shift();
        }
    }, 300);
});

onUnmounted(() => {
    if (intervalId) {
        clearInterval(intervalId);
        intervalId = null;
    }
});
</script>

<style scoped>
.home-container {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    position: relative;
}
</style>