<template>
    <div id="burger-table">
        <Message :msg="msg" v-show="msg" />
        <div id="burger-table-heading">
            <div class="order-id">#:</div>
            <div>Cliente</div>
            <div>Pão</div>
            <div>Carne</div>
            <div>Opcionais</div>
            <div>Ações</div>
        </div>
        <div id="burger-table-rows">
            <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
                <div class="order-number">{{ burger.id }}</div>
                <div>{{ burger.nome }}</div>
                <div>{{ burger.pao }}</div>
                <div>{{ burger.carne }}</div>
                <div>
                    <ul>
                        <li v-for="(opcional, index) in burger.opcionais" :key="index">{{ opcional }}</li>
                    </ul>
                </div>
                <div>
                    <select name="statos" class="status" @change="updateBurger($event, burger.id)">
                        <option value="">Selecione</option>
                        <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">{{ s.tipo }}</option>
                    </select>
                    <button id="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Message from './Message.vue';
export default {
    name: "Deshboard",
    components: {
        Message,
    },
    data(){
        return {
            burgers: null,
            burger_id: null,
            status: [],
            msg: ''

        }
    },
    methods: {
        async getPedidos(){

            const req = await fetch("http://localhost:3000/burgers");

            const data = await req.json();

            this.burgers = data;

            //resgatar status
            this.getStatus()
        },
        async getStatus(){
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();  

            this.status = data;
        },
        async deleteBurger(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: "DELETE"
            });


            const res = await req.json();

            //colocar msg sistema 
            this.msg = `Peido N° ${res.id} realizado com sucesso!`

            //limpar msg sistema
            setTimeout(() => this.msg ="", 3000 )
            window.location.href = "#msg"

            this.getPedidos();

        },
        async updateBurger(event, id){
            const option = event.target.value;

            const dataJson = JSON.stringify({ status : option });

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-Type" : "application/json" },
                body: dataJson,
            });

            const res = await req.json();

            this.msg = `Peido N° ${res.id} foi atualizado pra "${res.status}"!`

            //limpar msg sistema
            setTimeout(() => this.msg ="", 4000 )
            window.location.href = "#msg"
            this.getPedidos();
        }
    },
    mounted(){
        this.getPedidos();
    }
}
</script>

<style scoped>

    #burguer-table{
        width: 90%;
        margin: 0 auto;
    }

    #burger-table-heading,
    #burger-table-rows,
    .burger-table-row{
        display: flex;
        flex-wrap: wrap;
    }

    #burger-table-heading{
        font-weight: bold;
        padding: .5em;
        border-bottom: solid 3px #333;
    }

    #burger-table-heading div,
    .burger-table-row div{
        width: 18%;
    }

    .burger-table-row {
        width: 100%;
        padding: .5em;
        border-bottom: solid 1px #ccc;
    }

    #burger-table-heading .order-id,
    .burger-table-row .order-number{
        width: 5%;
    }

    select{
        padding: .5em .2em;
        margin-right: .9em;
        border-radius: 5px;
        border: solid 2px #222;
    }

    #delete-btn{
        padding: .5em .2em;
        background: #000;
        color: #FCBA03;
        font-weight: bold;
        border-radius: 5px;
        border: solid 2px #222;
        font-size: 1em;
        cursor: pointer;
        transition: .5s;
    }

    #delete-btn:hover{
        background: transparent;
        color: #222;
    }
</style>