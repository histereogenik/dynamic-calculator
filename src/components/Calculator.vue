<script setup>
    import { reactive } from 'vue';
    const props = defineProps(['operationType','calculateResult','operationResult','firstValue','secondValue','isResultVisible'])
    
    const state = reactive({
        operationType: 'addition',
        firstValue: null,
        secondValue: null,
        operationResult: null,
    })

    const isResultVisible = () => {
        return !isNaN(state.operationResult);
    }

    const calculateResult = () => {
        const { operationType } = state;

        switch(operationType) {
        case 'subtraction':
            return state.operationResult = state.firstValue - state.secondValue;
        case 'multiplication':
            return state.operationResult = state.firstValue * state.secondValue;
        case 'division':
            return state.operationResult = state.firstValue / state.secondValue;
        default:
            return state.operationResult = state.firstValue + state.secondValue;
        }
    }
</script>

<template>
    <div class="row g-0 align-items-center text-center">
        <div class="col-md-5">
            <input @keyup="calculateResult()" v-model.number="state.firstValue" class="fs-5 text-mobile" type="number" required placeholder="#first value" step=".01">
        </div>
        <div class="col-md-2 margin-mobile">
            <select @change="calculateResult()" v-model="state.operationType" class="form-control text-center fs-4 fw-bold">
            <option value="addition">+</option>
            <option value="subtraction">-</option>
            <option value="multiplication">x</option>
            <option value="division">/</option>
            </select>
        </div>
        <div class="col-md-5">
            <input @keyup="calculateResult()" v-model="state.secondValue" class="fs-5 text-mobile" type="number" required placeholder="#second value" step=".01">
        </div>
    </div>
    <div class="row text-center mt-4">
        <div class="col text-break">
            <span v-if="isResultVisible()" class="fs-1">{{ state.operationResult }}</span>
        </div>
    </div>
</template>

<style scoped>
    input[type=number]::-webkit-inner-spin-button, 
    input[type=number]::-webkit-outer-spin-button { 
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    margin: 0; 
}

.margin-mobile {
    @media (max-width: 767px) {
        margin: 8px 0;
    }
}

.text-mobile {
    @media (max-width: 767px) {
        text-align: center;
    }
}
</style>