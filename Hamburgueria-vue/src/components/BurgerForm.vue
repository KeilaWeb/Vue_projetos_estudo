<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="burger-form" @submit="createBurger">
                <div class="input-container">
                    <label for="nome">Nome do cliente</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
                </div>

                <div class="input-container">
                    <label for="pao">Escolha o pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>                    
                </div>

                <div class="input-container">
                    <label for="carne">Escolha o pão:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>                    
                </div>

                <div id="opcionais-container" class="input-container">
                    <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>                     
                </div>
                
                <div id="btn-form">
                    <input type="submit" class="submit-btn" value="Criar meu Burger">
                </div>

            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue'
export default {
    name: "BurgerForm",    
    data() {
        return {
            paes: [
                {
                "id": 1,
                "tipo": "Italiano Branco"
                },
                {
                "id": 2,
                "tipo": "3 Queijos"
                },
                {
                "id": 3,
                "tipo": "Parmesão e Orégano"
                },
                {
                "id": 4,
                "tipo": "Integral"
                }],

            carnes: [
                {
                "id": 1,
                "tipo": "Maminha"
                },
                {
                "id": 2,
                "tipo": "Alcatra"
                },
                {
                "id": 3,
                "tipo": "Picanha"
                },
                {
                "id": 4,
                "tipo": "Veggie burger"
                }],
                
            opcionaisdata:[
                {
                "id": 1,
                "tipo": "Bacon"
                },
                {
                "id": 2,
                "tipo": "Cheddar"
                },
                {
                "id": 3,
                "tipo": "Salame"
                },
                {
                "id": 4,
                "tipo": "Tomate"
                },
                {
                "id": 5,
                "tipo": "Cebola roxa"
                },
                {
                "id": 6,
                "tipo": "Pepino"
                }
            ],
            
            nome: null, //(singular) Dados enviado ao servidor->
            pao: null, // ->
            carne: null,
            opcionais: [], // ->
            status: "Solicitado", // ->
            msg: null,
            listaPedidos: JSON.parse(localStorage.getItem("resultado")) || [],
            msg: null,
            id: 1
            
        }
    },
    methods: {
        getIngredientes() {
            this.paes = data.paes
            this.carnes = data.carnes
            this.opcionais = data.opcional
        },
        createBurger(e){
            e.preventDefault();// para fazer com que o evento pare de ser executado
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcional: Array.from(this.opcionais),
                status: "Solicitado",
                id: this.listaPedidos.length + 1, // Calcular ID dinamicamente
            }
            
            this.listaPedidos.push(data);
            localStorage.setItem("resultado", JSON.stringify(this.listaPedidos));
            this.id++

            //mensagem do sistema
            this.msg = `${data.nome}, seu pedido foi realizado com sucesso`

            //limpar mensagem
            setTimeout(() => this.msg= "", 3000);

            //limpar os campos 
            this.nome = null;
            this.carne = null;
            this.pao = null;
            this.opcionais = [];           
        }
    },
    components: {
        Message
    }
}
</script>


<style scoped>
    #burger-form {    
        max-width: 400px;
        margin: 0 auto;
        align-items: flex-start;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 18px;
    }
    label {
        font-weight: bold;        
        margin-bottom: 10px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #E4700C;
    }

    input, select {
        padding: 8px 15px;
        width: 300px;
        border-radius: 20px;
        border-top: 1px solid #e4710c17;
        border-left: 1px solid #e4710c9d;
        border-right: 1px solid #e4710c9d;
        border-bottom: 3px solid #e4710c9d;
    }

    #opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span, 
    .checkbox-container input {
        width: auto;

    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    div#btn-form {
        width: auto;
        width: 100%;
        margin-bottom: 50px;
    }

    .submit-btn {
        padding: 14px 40px;
        margin: 0 auto;
        border-radius: 100px;
        background-color: #E4700C;
        color: #f7f7f7;
        font-weight: bold;
        font-size: 18px;
        line-height: 1em;
        cursor: pointer;
    }

    .submit-btn:hover {
    background-color: #f7f7f7;
    color: #E4700C;
    transition: all 0.3s;
  }

</style>
