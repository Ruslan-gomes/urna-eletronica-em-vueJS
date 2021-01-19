<template>
    <div class="urna-teclado">
        <div class="urna-teclado-numerico">
            <div class="urna-teclado-numerico-linhas">
                <button @click="adicionarNumero(1)">1</button>
                <button @click="adicionarNumero(2)">2</button>
                <button @click="adicionarNumero(3)">3</button>
            </div>
            <div class="urna-teclado-numerico-linhas">
                <button @click="adicionarNumero(4)">4</button>
                <button @click="adicionarNumero(5)">5</button>
                <button @click="adicionarNumero(6)">6</button>
            </div>
            <div class="urna-teclado-numerico-linhas">
                <button @click="adicionarNumero(7)">7</button>
                <button @click="adicionarNumero(8)">8</button>
                <button @click="adicionarNumero(9)">9</button>
            </div>
            <div class="urna-teclado-numerico-linhas">
                <button @click="adicionarNumero(0)">0</button>
            </div>
        </div>

        <div class="urna-teclado-acoes">
            <button @click="votoBranco" class="btn-branco">BRANCO</button>
            <button @click="corrigir" class="btn-corrige">CORRIGE</button>
            <button @click="confirmar" class="btn-confirma">CONFIRMA</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'teclado',
    props: {
        adicionarNumero: Function,
        corrigir: Function,
        confirmar: Function,
        votoBranco: Function
    }
}
</script>


<style scoped>

.urna-teclado{
    width: 40%;
    height: 100%;
    background-color: var(--ballot-box-keyboard-color);
    border-radius: 5px;
    padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
}

.urna-teclado-numerico{
    widows: 100%;
}

.urna-teclado-numerico-linhas{
    display: flex;
    justify-content: space-around;
    margin-bottom: 20px;
}

.urna-teclado-numerico button{
    background-color: var(--ballot-box-keyboard-button-color);
    color: var(--light-text-color);
    font-size: 30px;
    border-radius: 5px;
    width: 80px;
    height: 50px;
}

.urna-teclado-acoes{
    width: 100%;
    display: flex;
    justify-content: space-around;
}

.urna-teclado-acoes button{
    color: var(--dark-text-color);
    font-size: 15px;
    border-radius: 5px;
    width: 30%;
    height: 50px;
}

.btn-branco{
    background-color: var(--ballot-box-white-button-color);
}

.btn-corrige{
    background-color: var(--ballot-box-correct-button-color);
}

.btn-confirma{
    background-color: var(--ballot-box-confirm-button-color);
}
</style>