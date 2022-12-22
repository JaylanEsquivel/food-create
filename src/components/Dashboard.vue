<template>
    <Message :msg="msg" v-show="msg" />

    <div id="table-burguer">
        <div id="table-header">
            <div class="order-id">ID</div>
            <div>CLIENTE</div>
            <div>PÃO</div>
            <div>CARNE</div>
            <div>OPCIONAIS</div>
            <div>AÇÕES</div>
        </div>
        <div id="table-rows">
            <div class="table-row" v-for="burguer in burguers" :key="burguer.id">
                <div class="order-number">{{burguer.id}}</div>
                <div>{{burguer.nome}}</div>
                <div>{{burguer.pao}}</div>
                <div>{{burguer.carne}}</div>
                <div>
                    <ul>
                        <li v-for="(op,index) in burguer.opcionais" :key="index">{{op}}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" id="status" @change="updateBurguer($event, burguer.id)">
                        <option v-for="s in status" :key="s.id" :selected="burguer.status == s.tipo" :value="s.tipo">{{s.tipo}}</option>
                    </select>
                    <button class="cancelar-btn" @click="deletarBurguer(burguer.id);">Cancelar</button>
                </div>

            </div>
        </div>

    </div>

</template>

<script>
    import Message from './Message.vue';

    export default {
        name: 'Dashboard',
        components: {
            Message
        },
        data() { 
            return {
                burguers: null,
                buguer_id: null,
                status: [],
                msg: null
            }
        },
        methods: {
            async getPedidos() { 

                const req = await fetch("http://localhost:3000/burgers");

                const data = await req.json();

                this.burguers = data;

            },
            async getStatus() { 
                const req = await fetch("http://localhost:3000/status");

                const data = await req.json();

                this.status = data;

            },
            async updateBurguer(event, id) {

                const option = event.target.value;

                const datajson = JSON.stringify({ status: option });
                const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                    method: "PATCH",
                    headers: { "Content-type": "application/json" },
                    body: datajson
                });

                const resposta = await req.json();

                this.msg = `Pedido N° ${id} foi Atualizado com Sucesso para ${option}`;

                setTimeout(() => this.msg = "", 5000);


            },
            async deletarBurguer(id) { 

                const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                    method: 'DELETE'
                });

                const resposta = await req.json();

                this.msg = `Pedido N° ${id} removido com Sucesso!`;

                setTimeout(() => this.msg = "", 5000);

                this.getPedidos();
            }
        },
        mounted() {
            this.getPedidos();
            this.getStatus();
        }
    }
</script>

<style scoped>

    #table-burguer{
        max-width: 1200px;
        margin: 0px auto;
    }

    #table-header,
    #table-rows,
    .table-row{
        display: flex;
        flex-wrap: wrap;
    }

    #table-header{
        font-weight: bold;
        padding: 10px;
        border-bottom: 2px solid #333;
    }

    #table-header div,
    .table-row div{
        width: 18%;
    }
    .table-row{
        width: 100%;
        padding: 12px;
        border-bottom: 2px solid #ccc;
    }

    #table-header .order-id,
    .table-row .order-number{
        width: 5%;
    }

    select{
        padding: 5px 6px;
        margin-right: 12px; 
    }
    .cancelar-btn{
        background-color: #222;
        color: #f2ba0d;
        cursor: pointer;
        padding: 6px;
        margin: 0 auto;
        border: 2px solid #222;
        font-size: 12px;
        transition: .5s;
        width: auto;
    }   

    .cancelar-btn:hover{
        background-color: transparent;
        color: #222;
    }

</style>