<template>
    <div id="burger-main">
        <Message :msg="msg" v-show="msg" />

        <div>
            <form id="burguer-from" @submit="createBurguer($event)">
                <div class="input-container">
                    <label for="nome">Nome do cliente</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome"/>
                </div>
                <div class="input-container">
                    <label for="pao">Escolha seu pão:</label>
                    <select name="pao" id="pao" v-model="pao" >
                        <option value="">Selecione o tipo de pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo" >{{ pao.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="carne">Escolha a carne do seu Burguer:</label>
                    <select name="carne" id="carne" v-model="carne" >
                        <option value=""  >Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo" >{{ carne.tipo }}</option>
                    </select>
                </div>
                <div id="opcionais-container" class="input-container">
                    <label for="nome">Selecione os Opcionais:</label>
                    <div class="checkbox-container" v-for="opcao in opcionaisdata" :key="opcao.id">
                        <input type="checkbox" :id="'checkbox'+opcao.id" name="opcionais" v-model="opcionais" :value="opcao.tipo">         
                        <label  :for="'checkbox'+opcao.id">{{ opcao.tipo}}</label>
                    </div>
                </div>
                <div class="input-container">
                    <button type="submit" class="submit-btn" value="">Criar meu Burguer</button>
                </div>
            </form>
        </div>

    </div>
</template>
<script>
    import Message from './Message.vue';

    export default {
        name: 'BurguerForm',
        components: {
            Message
        },
        data(){
            return {
                paes: null,
                carnes: null,
                opcionaisdata: null,
                nome: null,
                pao: null,
                carne: null,
                opcionais: [],
                msg: null
            }
        },
        methods: {
            async getIngredientes() { 
                const req = await fetch("http://localhost:3000/ingredientes");
                const data = await req.json();

                this.paes = data.paes;
                this.carnes = data.carnes;
                this.opcionaisdata = data.opcionais;
            },
            async createBurguer(e) { 
                e.preventDefault();

                const data = {
                    nome: this.nome,
                    pao: this.pao,
                    carne: this.carne,
                    opcionais: Array.from(this.opcionais),
                    status: "Solicitado"
                }

                //console.log(data);

                const datajson = JSON.stringify(data);

                const req = await fetch("http://localhost:3000/burgers", {
                    method: "POST",
                    headers: { "Content-type": "application/json" },
                    body: datajson   
                });

                const resposta = await req.json();

                this.msg = `Pedido N° ${resposta.id} realizado com Sucesso!`;

                setTimeout(() => this.msg = "", 3000);

                this.nome = "";
                this.pao = "";
                this.carne = "";
                this.opcionais = [];

                console.log(resposta);

            }
        },
        mounted() { 
            this.getIngredientes();
        }
    }
</script>
<style scoped>

    #burguer-from{
        max-width: 400px;
        margin: 0 auto;
    }
    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 3px #f2ba0d solid;
    }

    input, select{
        padding: 5px 10px;
        width: 100%;
    }

    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    .checkbox-container{
        display:flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }
    .checkbox-container label{
        width: 100%;
    }

    .checkbox-container label ,
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container label {
        margin-left: 5px;
        margin-bottom: 0px;
        font-weight: bold;
        border-left: none;
        padding: 0px !important;    
        cursor: default;
        -webkit-touch-callout: none;
        -webkit-user-select: none;
        -khtml-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }

    .submit-btn{
        background-color: #222;
        color: #f2ba0d;
        cursor: pointer;
        padding: 10px;
        margin: 0 auto;
        border: 2px solid #222;
        font-size: 16px;
        transition: .5s;
        width: 100%;
    }   

    .submit-btn:hover{
        background-color: transparent;
        color: #222;
    }
</style>