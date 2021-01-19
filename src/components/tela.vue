<template>
    <div class="urna-tela">

        <div v-if="tela != 'fim'" class="urna-tela-voto">
            <div class="urna-tela-voto-textos">
                <div class="urna-tela-voto-textos-titulo">Seu voto para:</div>
                <div class="urna-tela-voto-tipo">{{tela}}</div>
            </div>

            <div class="urna-tela-voto-numeros">
                Números:
                <div class="urna-tela-voto-numero" v-for="(value, key) in numeroVoto.padEnd(quantidadeNumeros, ' ')" :key="key">
                    {{value}}
                </div>                
            </div>

            <div class="urna-tela-voto-descricoes">
                <div class="urna-tela-voto-descricao">
                Nome:  {{candidato.nome ? candidato.nome : '______________ '}}
            </div>

            <div class="urna-tela-voto-descricao">
                 Partido:  {{candidato.partido ? candidato.partido : '______________ '}}
            </div>
            </div>
                <div v-if="candidato.imagem" class="urna-tela-voto-imagem">
                <img :src="candidato.imagem" alt="imagem do candidato">
            </div>
        </div>
        <div v-if="tela == 'fim'" class="urna-tela-fim">
            FIM
        </div>

    </div>
</template>

<script>
export default {
    name: 'tela',
    props: {
        tela: String,
        numeroVoto: String,
        quantidadeNumeros: Number,
        candidato: Object
    }
}
</script>

<style scoped>
.urna-tela{
    width: 55%;   
    height: 100%;
    background-color: var(--ballot-box-screen-color);
    border-radius: 5px;
    border-color: 2px solid var(--light-border-color);
    padding: 20px;
    color: var(--dark-text-color);
}

.urna-tela-voto{
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
}

.urna-tela-voto-textos{
    flex: 1;
}

.urna-tela-voto-tipo{
    font-size: 50px;
    margin: 10px 20px;
}

.urna-tela-voto-numeros{
    display: flex;
    align-items: center;
}

.urna-tela-voto-numero{
    width: 45px;
    height: 55px;
    border: 1px solid var(--dark-border-color);
    margin-left: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 30px;
}

.urna-tela-voto-descricoes{
    display: flex;
    flex-direction: column;
}

.urna-tela-voto-descricao{
    margin-top: 20px;
}

.urna-tela-voto-imagem img{
    width: 110px;
    height: 150px;
    border: 1px solid var(--dark-border-color);
    float: right;
}

.urna-tela-fim{
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 120px;
    width: 100%;
    height: 100%;
}
</style>