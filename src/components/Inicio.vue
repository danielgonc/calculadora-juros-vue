<template>
    <div id="app">
        <div class="esquerda">
            <div class="wrapper">
                <h2>{{nomeForm}}</h2>
                <form v-on:submit="submitForm">
                    <label for="jurosMesEle" class="label-padrao">Juros por mes</label>
                    <input id="jurosMesEle" v-model="jurosMes" type="number" class="input-padrao" required>

                    <label for="multaAtrasoEle" class="label-padrao">Multa por atraso</label>
                    <input id="multaAtrasoEle" v-model="multaAtraso" type="number" class="input-padrao" required>

                    <label for="valorMenEle" class="label-padrao">Valor da mensalidade</label>
                    <input id="valorMenEle" v-model="valorMen" type="number" class="input-padrao" required>

                    <label for="dataVencimentoEle" class="label-padrao">Data de vencimento</label>
                    <div class="campos-data">
                        <input id="dataVencimentoEle" v-model.lazy="dataVencimento" type="date" class="input-padrao" required>
                        <span class="span-data" v-on:click="dataVencimento = obterDataAtual()">Hoje</span>
                    </div>
                    <label for="dataHojeEle" class="label-padrao">Data de hoje</label>
                    <div class="campos-data">
                        <input id="dataHojeEle" v-model="dataHoje" type="date" class="input-padrao" required>
                        <span class="span-data" v-on:click="dataHoje = obterDataAtual()">Hoje</span>
                    </div>
                    
                    
                    <button class="btn-submeter">Enviar</button>
                </form>
            </div>
        </div>
        <div class="direita">
            <div class="wrapper">
                <TabelaResultado v-bind:titulo="nomeTabela" 
                                :multaAtraso="multaAtrasoCalculado" 
                                :diasAtrasados="diasAtrasados"
                                :jurosCalculado="jurosCalculado"
                                :totalPagar="totalPagar"></TabelaResultado>
            </div>
        </div>
    </div>
</template>
<script>
import TabelaResultado from '../components/TabelaResultado.vue';
export default {
    name: "app",
    data(){
        return {
            nomeForm: "Dados Iniciais",
            jurosMes: '',
            multaAtraso: '',
            valorMen: '',
            dataHoje: '',
            dataVencimento: '',
            nomeTabela: 'Resultado',
            multaAtrasoCalculado: '',
            diasAtrasados: '',
            jurosCalculado: '',
            totalPagar: ''
        }
    },
    components:{
        TabelaResultado
    },
    methods: {
        submitForm: function (e){
            e.preventDefault();
            this.diasAtrasados = this.calcularDiferencaDeDias();
            this.valorMen = parseFloat(this.valorMen);
            if(this.diasAtrasados > 0){

                this.multaAtrasoCalculado = parseFloat(((this.multaAtraso/100)*this.valorMen).toPrecision(1));

                let juroPorDia = parseFloat((parseFloat(this.jurosMes/30)/100).toPrecision(1));
                this.jurosCalculado = parseFloat(this.diasAtrasados * (juroPorDia * this.valorMen));
                this.totalPagar = this.jurosCalculado + this.multaAtrasoCalculado + this.valorMen;
            }else{
                this.multaAtrasoCalculado = 0;
                this.jurosCalculado = 0;
                this.totalPagar = this.valorMen;
            }

        },
        obterDataAtual: function(){
            let data = new Date(Date.now());
            data = `${data.getFullYear()}-${("0" + (data.getMonth() + 1)).slice(-2)}-${("0" + data.getDate()).slice(-2)}`;
            return data;
        },
        calcularDiferencaDeDias: function(){
            let dataHoje = new Date(this.dataHoje);
            let dataVencimento = new Date(this.dataVencimento);

            if(dataVencimento < dataHoje)
                return 0;
            else{
                let diffHr = Math.abs(dataHoje.getTime() - dataVencimento.getTime());
                let diferencaDias = Math.ceil(diffHr / (1000 * 3600 * 24)); 
                return diferencaDias;
            }
        }
    }
}
</script>

<style>
.esquerda{
    width: 50%;
    float: left;
    text-align: center;
    align-items: center;
}
.direita{
    width: 50%;
    float: right;
    text-align: center;
    align-items: center;
}
.wrapper{
    width: 60%;
    display: inline-block;
}
.label-padrao{
    width: 100%;
    display: inline-block;
}
.input-padrao{
    width: 50%;
    display: inline-block;
    height: 24px;
}
.campos-data{
    position: relative;
}
.span-data{
    background-color: #000;
    height: 25px;
    border-radius: 5px;
    text-align: center;
    vertical-align: middle;
    padding: 11px 10px 0 10px;
    display: inline-block;
    color: #fff;
    font-size: 13px;
    position: absolute;
    top: 1px;
    right: 0;
    cursor: pointer;
    transition: all 0.3s;
}
.btn-submeter{
    width: 55%;
    height: 35px;;
    margin-top: 25px;
    background-color: #000;
    border: none;
    border-radius: 4px;
    color: #fff;
    cursor: pointer;
    transition: all 0.3s;
}
.btn-submeter:hover, .span-data:hover{
    background-color: #888
}
</style>
