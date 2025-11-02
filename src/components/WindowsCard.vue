<template>
    <div class="WindowsCard" :style="{ backgroundColor: bodyBgColor }">
        <div class="cardHeader">
            <div class="cardTitle">{{ title }}</div>
        </div>

        <div class="cardBody">{{ bodyContent }}</div>
    </div>
</template>

<script setup>
defineProps({
    bodyBgColor: {
        type: String,
        default: '#f0f0f0'
    },
    bodyContent: {
        type: String,
        default: '内容内容'
    }
});

const title = '温馨提示';

</script>