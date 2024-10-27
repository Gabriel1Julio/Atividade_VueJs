<script setup>
    import { reactive, watch } from 'vue';

    const estado = reactive({
        numero1: '',
        numero2: '',
        expressao: 'soma',
        resultado: '',
    })

function calcular() {
    const numero1 = parseFloat(estado.numero1);
    const numero2 = parseFloat(estado.numero2);
    if (isNaN(numero1) || isNaN(numero2)) {
        return;
    }
    let resultado;

    switch (estado.expressao) {
        case 'soma':
        resultado = numero1 + numero2;
        break;
        case 'subtracao':
        resultado = numero1 - numero2;
        break;
        case 'multiplicacao':
        resultado = numero1 * numero2;
        break;
        case 'divisao':
        if (numero2 === 0 || numero1 === 0) {
            estado.resultado = 'Não existe divisão por 0!';
            return;
        } else {
            resultado = numero1 / numero2;
        }
        break;
    }

    estado.resultado = resultado; 
}

watch(
    () => [estado.numero1, estado.numero2, estado.expressao],
    calcular
);
</script>

<template>
    <header>
        <h1>
        Calculadora Aritimética
        </h1>
    </header>

    <div class="main">
        <input v-model="estado.numero1" class="number1" type="number" placeholder="Digite um número">
        <select v-model="estado.expressao" id="expressao">
            <option value="soma">+</option>
            <option value="subtracao">-</option>
            <option value="multiplicacao">x</option>
            <option value="divisao">÷</option>
        </select>
        <input v-model="estado.numero2" class="number2" type="number" placeholder="Digite um número">
        <h3>Resultado</h3>
        <div class="resultado"><p>{{ estado.resultado }}</p></div> 
    </div>
</template>

<style scoped>

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    }

    header {
    text-align: center;
    padding: 20px;
    }

    .main {
    margin-top: 50px;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    }

    .number1 {
    padding: 10px;
    text-align: center;
    width: 10%;
    margin-bottom: 15px;
    }

    .number2 {
    padding: 10px;
    text-align: center;
    width: 10%;
    margin-top: 15px;
    }

    .resultado {
    margin-top: 20px;
    padding: 10px;
    width: 180px;
    height: 50px;
    text-align: center;
    border: 1px solid black;
    }

    h3 {
    margin-top: 30px;
    }

</style>
