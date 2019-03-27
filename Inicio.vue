<template>
    <div id="app">
        <div class="esquerda">
            <h1>{{nomeForm}}</h1>
            <form v-on:submit="submitForm">
                <label for="jurosMesEle" class="label-padrao">Juros por mes</label>
                <input id="jurosMesEle" v-model="jurosMes" type="number" class="input-padrao">

                <label for="multaAtrasoEle" class="label-padrao">Multa por atraso</label>
                <input id="multaAtrasoEle" v-model="multaAtraso" type="number" class="input-padrao">

                <label for="valorMenEle" class="label-padrao">Valor da mensalidade</label>
                <input id="valorMenEle" v-model="valorMen" type="number" class="input-padrao">

                <label for="dataVencimentoEle" class="label-padrao">Data de vencimento</label>
                <input id="dataVencimentoEle" v-model="dataVencimento" type="date" class="input-padrao">

                <label for="dataHojeEle" class="label-padrao">Data de hoje</label>
                <input id="dataHojeEle" v-model="dataHoje" type="date" class="input-padrao">
                
                <button class="btn-submeter">Enviar</button>
            </form>
        </div>
    </div>
</template>
<script>
export default {
    name: "app",
    data: function(){
        return {
            nomeForm: "Dados Iniciais",
            jurosMes: '',
            multaAtraso: '',
            valorMen: '',
            dataHoje: '',
            dataVencimento: '',
        }
    },
    methods: {
        submitForm: function (e){
            e.preventDefault()

        }
    }
}
</script>

<style>
.esquerda{
    width: 50vw;
    float: left; 
}
.label-padrao{
    width: 50%;
    display: inline-block;

}
.input-padrao{
    width: 50%;
    display: inline-block;
    height: 24px;

}
.btn-submeter{
    width: 50%;
    height: 35px;;
    margin-top: 25px;
    background-color: #000;
    border: none;
    border-radius: 4px;
    color: #fff;
    cursor: pointer;
    transition: all 0.3s;
}
.btn-submeter:hover{
    background-color: #888
}
</style>
