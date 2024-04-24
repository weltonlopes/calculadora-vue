<script setup>
import { reactive } from 'vue';
    
    let selectedOption;
    let primeiroNumero;
    let segundoNumero;
    let calculo = function(n1, n2) {
        return n1 + n2;
    };

    const estado = reactive({
        resultado: 0,
        label1: "Parcela 1",
        label2: "Parcela 2",
        labelResult: "A soma é",
    })


    const calcular = () => {
        primeiroNumero = document.getElementById('input1').value;
        segundoNumero = document.getElementById('input2').value;

        if(primeiroNumero && segundoNumero) {
            // se for divisão, previnir a divisão por 0
            primeiroNumero = parseFloat(primeiroNumero);
            segundoNumero = parseFloat(segundoNumero);
            if(selectedOption == 3 && segundoNumero == 0) {
                    estado.resultado = "Não é possível dividir por 0";
            } else {
                estado.resultado = calculo(primeiroNumero, segundoNumero);
            }
        } else {
            estado.resultado = "falta preencher um campo.";
        }
    }

    const mudarLabels = () => {
        if(selectedOption == 0) {
            estado.label1 = "Parcela 1";
            estado.label2 = "Parcela 2";
            estado.labelResult = "A soma é";
        } else if(selectedOption == 1) {
            estado.label1 = "Minuendo";
            estado.label2 = "Subtraendo";
            estado.labelResult = "O resto é";
        } else if(selectedOption == 2) {
            estado.label1 = "Fator 1";
            estado.label2 = "Fator 2";
            estado.labelResult = "O produto é";
        } else {
            estado.label1 = "Dividendo";
            estado.label2 = "Divisor";
            estado.labelResult = "O resultado é";
        }
    }

    const definirCalculos = () => {
        
        if(selectedOption == 0) {
            calculo = function(n1, n2) {
                return n1 + n2;
            }
        } else if(selectedOption == 1) {
            calculo = function(n1, n2) {
                return n1 - n2;
            }
        } else if(selectedOption == 2) {
            calculo = function(n1, n2) {
                return n1 * n2;
            }
        } else {
            calculo = function(n1, n2) {
                return n1 / n2;
            }
        }
    }

    const onChange = (event) => {
        selectedOption = event.srcElement.options.selectedIndex;
        mudarLabels();
        definirCalculos();
        calcular();
    };

</script>

<template>
    <div class="container">
        <h3>Calculadora com VueJs</h3>
        <form class="mt-4">
            <label class="form-label" for="operacao">
                Selecione a operação
                <select @change="onChange" class="form-select" name="operacao" id="selecionador">
                    <option value="adicao">Adição</option>
                    <option value="subtracao">Subtração</option>
                    <option value="multiplicacao">Multiplicação</option>
                    <option value="divisao">Divisão</option>
                </select>
            </label>
            <div class="mb-3 d-flex">
                <label class="form-label" for="input1"> <span id="label_input1">{{ estado.label1 }}</span>
                    <input @change="calcular" class="form-control me-2" type="number" name="input1" id="input1">
                </label>
                <label class="form-label" for="input2"> <span id="label_input2">{{ estado.label2 }}</span>
                    <input @change="calcular" class="form-control" type="number" name="input2" id="input2">
                </label>
            </div>
            <h2 class="form-text">{{estado.labelResult + ': ' + estado.resultado}}</h2>
        </form>
    </div>
</template>

<style scoped>
</style>
