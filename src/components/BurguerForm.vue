<template>
    <div id="burger-main">
        <p>Componete de mensagem</p>

        <div>
            <form id="burguer-from">
                <div class="input-container">
                    <label for="nome">Nome do cliente</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome"/>
                </div>

                <div class="input-container">
                    <label for="pao">Escolha seu pão:</label>
                    <select name="pao" id="pao" v-model="pao" >
                        <option value="" selected  disabled>Selecione o tipo de pão</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="carne">Escolha a carne do seu Burguer:</label>
                    <select name="carne" id="carne" v-model="carne" >
                        <option value="" selected  disabled >Selecione o tipo de carne</option>
                    </select>
                </div>
                <div id="opcionais-container" class="input-container">
                    <label for="nome">Selecione os Opcionais:</label>
                    <div class="checkbox-container">
                        <input type="checkbox" name="opcionais" v-model="opcionais" value="Salame">         
                        <span>Salame</span>
                    </div>
                    <div class="checkbox-container">
                        <input type="checkbox" name="opcionais" v-model="opcionais" value="Salame">         
                        <span>Salame</span>
                    </div>
                    <div class="checkbox-container">
                        <input type="checkbox" name="opcionais" v-model="opcionais" value="Salame">         
                        <span>Salame</span>
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
    export default {
        name: 'BurguerForm'
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

    .checkbox-container span,
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container span{
        margin-left: 5px;
        font-weight: bold;
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