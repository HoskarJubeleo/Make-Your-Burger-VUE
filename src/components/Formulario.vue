<template>
    <div id="main_form">
        <Message :msg="msg" v-show="msg" />
        <div>
            <form action="" id="burger-form" @submit="createBurger">
                <div class="input-container">
                    <label for="nome">Nome do Cliente</label>
                    <input type="text" name="nome" id="nome_input" v-model="nome" placeholder="Digite seu nome" required>
                </div>

                <div class="input-container">
                    <label for="pao">Escolha o Pão</label>
                    <select name="pao" id="pao" v-model="pao" required>
                        <option disabled>Selecione o Pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="carne">Escolha a Carne</label>
                    <select name="carne" id="carne" v-model="carne" required>
                        <option disabled selected>Selecione a Carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                </div>

                <div id="optionais-container" class="input-container">
                    <label id="optionais-title" for="opcionais">Selecione os Opcionais</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{opcional.tipo}}</span>
                    </div>
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Cadastrar Pedido">
                </div>
            </form>
        </div>
    </div>
</template>

<script lang="ts">

import Message from './Message.vue'
import MessageError from './MessageError.vue'
 
export default {
    name: "Formulario",
    components:{
        Message,
        MessageError,
    },

    data() {
        return {
            //dados do server
            paes: null,
            carnes: null,
            opcionaisdata: null,
            //dados enviados
            nome:null,
            pao: null,
            carne: null,
            opcionais: [],
            msg: null,
        }
    },
    methods:{
        async getIngredientes(){
            
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();

            this.paes = data.paes;

            this.carnes = data.carnes;

            this.opcionaisdata = data.opcionais;

        },
        async createBurger(e){
            e.preventDefault()
            
/*            var NomeInput = document.querySelector("#nome_imput")

            if(NomeInput == null){
                alert('')
                return
            } */

            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers",{
                method: "POST", 
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            //colocar msg sistema 
            this.msg = `Peido N° ${res.id} realizado com sucesso!`

            //limpar msg sistema
            setTimeout(() => this.msg ="", 3000 )

            //limpar os campos
            this.nome = "";
            this.pao = "";
            this.carne = "";
            this.opcionais = "";

        }
    },
    mounted(){
        this.getIngredientes()
    }

}
</script>

<style scoped>
    #main_form{
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-weight: 500;
        margin-bottom: .5em;
        color: #222;
        border-left: solid 4px #000;
    }

    input, select{
        padding: .5em 1em;
        widows: 90%;
        border: solid 2px #222;
        border-radius: 5px;
        outline: none;
    }

    #optionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    #optionais-title{
        width: 100%;
    }

    .checkbox-container{
        display: flex;
        align-content: flex-start;
        width: 40%;
        margin-bottom: 20px;
        margin-left: 10%;
    }

    .checkbox-container span, .checkbox-container input{
        width: auto;

    }

    .checkbox-container span{
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn{
        margin: 0 auto;
        margin-bottom: 1.5em;
        font-size: 1em;
        padding: .8em;
        border: solid 2px #222;
        border-radius: 5px;
        background: #222;
        color: #FCBA03;
        font-weight: bold;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover{
        background: transparent;
        color: #222;

    }
</style>