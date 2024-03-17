<template>
    <div id="cabecalho"></div>
    <div id="burger-table">   
        <Message :msg="msg" v-show="msg" />     
        <h1>Gerenciar Pedidos:</h1>
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div class="burger-table-row" 
                v-for="burger in burgers" 
                :key="burger.id">
                <div class="order-number">{{ burger.id }}</div>
                    <div>{{ burger.nome }}</div>
                    <div>{{ burger.pao }}</div>
                    <div>{{ burger.carne }}</div>
                    <div>
                        <ul 
                            v-for="opcional, index in burger.opcional" :key="index"
                        >
                            <li>{{ opcional }}</li>
                        </ul>
                    </div>
                    <div>
                        <select name="status" 
                            class="status" 
                            @change="updateBurger(burger.id, $event.target.value)"
                            v-model="burger.status" >                       
                            <option v-for="status in statusdata" :key="status.id" :value="status.tipo">   
                                    {{ status.tipo }}
                            </option>
                        </select>
                    <button
                        class="delete-btn"
                        @click="deleteBurger(burger.id)"
                    >
                        Deletar
                    </button>
                </div>
            </div>
            
        </div>
    </div>
</template>

<script>
import Message from './Message.vue'

export default {    
    name: "Dashboard",
    data() {
        return {            
            statusdata: [
                {
                    "id": 1,
                    "tipo": "Solicitado"
                },
                {
                    "id": 2,
                    "tipo": "Em produção"
                },
                {
                    "id": 3,
                    "tipo": "Finalizado"
                }
            ],
            burgers: null,
            burger_id: null,
            msg: null,
        }
    },
    components: {
        Message
    },
    methods: {
        getPedidos() {
            this.burgers = JSON.parse(localStorage.getItem("resultado"));      
        },
        getStatus(){
            this.status = "Solicitado";     
        },
        deleteBurger(id){
            // Filtrar os pedidos para remover o pedido com o ID correspondente, criando um novo array
            this.burgers = this.burgers.filter(burger => burger.id !== id);  
            
            localStorage.setItem("resultado", JSON.stringify(this.burgers));// Atualizar o localStorage   
            
            //mensagem do sistema
            this.msg = `Pedido removido com sucesso`
            //limpar mensagem
            setTimeout(() => this.msg= "", 3000);

        },
        updateBurger(id, selectedStatus) {
            const burgerToUpdate = this.burgers.find((burger) => burger.id === id);
            burgerToUpdate.status = selectedStatus;
            this.updateLocalStorage();
        },
        updateLocalStorage() {
            localStorage.setItem("resultado", JSON.stringify(this.burgers));

            //mensagem do sistema
            this.msg = `O pedido foi atualizado`;
            setTimeout(() => this.msg= "", 3000);
        },

    },
    mounted() {
        this.getStatus();
        this.getPedidos();
    }
}
</script>



<style scoped>
    #cabecalho {
        margin: -200px 0px 0px 0px;
        height: 120px;
        background-color: #792F20;
    }

    #burger-table {
        max-width: 1200px;
        height: 745px;
        padding:  90px 0px;
        margin: 0 auto;
    }

    h1 {
        line-height: 2em;
        color: #792F20;
    }

    #burger-table-heading,
    #burger-table-rows,
    .burger-table-row{
        color: #792F20;
        display: flex;
        flex-wrap: wrap;
    }

    #burger-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #E4700C;        
    }

    #burger-table-heading div,
    .burger-table-row div {
        
        width: 19%;
    }

    .burger-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }

    #burger-table-heading .order-id,
    .burger-table-row .order-number {
        width: 5%;
    }

    select {
        padding: 12px 6px;
        margin-right: 12px;
        border-radius: 8px;
    }

    .delete-btn {
        background-color: #E4700C;
        color: #fff ;
        font-weight: bold;
        border: 2px solid #792F20;
        padding: 12px;
        border-radius: 8px;
        font-size: 14px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover {
        background-color: transparent;
        color: #E4700C;
    }

</style>