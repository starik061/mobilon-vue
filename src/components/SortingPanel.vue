<template>
    <v-container :style="`background: ${bgColor}`">
        <!-- <v-row align="center" justify="center">
            <h2 class="title">Панель сортировки</h2>
        </v-row> -->

        <v-row align="center" justify="center">
            <v-col v-for="(btnInfo, btnInfoIdx) in sortingButtonsDataArray" :key="btnInfoIdx" cols="auto">
                <v-btn class="sort-btn" :class="{ 'active-btn': sortType === btnInfo.type && isListNotEmpty }"
                    density="comfortable" :icon="btnInfo.icon" :title="btnInfo.type"
                    @click="handleSortBtnClick(btnInfo.type)"></v-btn>
            </v-col>
        </v-row>
    </v-container>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
    bgColor: {
        type: String,
        required: true
    },
    borderShadowID: {
        type: Number,
        required: true
    },
    sortType: {
        type: Number,
        default: "Без сортировки"
    },
    isListNotEmpty: {
        type: Boolean,
        default: true
    }
});

const emit = defineEmits(['sort']);

const sortingButtonsDataArray = ref([
    { type: "Без сортировки", icon: "mdi-sort-variant-off" },
    { type: "По возрастанию рейтинга", icon: "mdi-sort-reverse-variant" },
    { type: "По убыванию рейтинга", icon: "mdi-sort-variant" }]);

const borderShadowColor = computed(() => {
    return props.borderShadowID === 1 ? 'blue' : props.borderShadowID === 2 ? 'yellow' : 'pink';
});

function handleSortBtnClick(sortType) {
    emit("sort", sortType)
}
</script>

<style lang="scss" scoped>
.title {
    padding-bottom: 10px;
    width: 90%;
    display: flex;
    align-items: center;
    justify-content: center;
    border-bottom: 2px solid white;
}

.sort-btn {
    opacity: 0.5;

    &:hover,
    &:active,
    &:focus {
        box-shadow: 0px 0px 27px 0px v-bind('borderShadowColor');
        opacity: 1;
    }

    &.active-btn {
        opacity: 1;
        box-shadow: 0px 0px 27px 0px v-bind('borderShadowColor');
    }
}
</style>