<template>
    <div id="nav">
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
        <router-link to="/">Home</router-link>
        <router-link to="/pedidos">Pedidos</router-link>
    </div>
</template>

<script>
export default {
    name: "Navegacao",
    props: ["logo", "alt"]
}
</script>

<style scope>
    #nav {       
        z-index: 10;
        background-color: #ffffff00;
        padding: 20px 300px 0px 300px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        
    }
    #nav #logo-url {
        margin: auto;
        margin-left: 0;
    }
    #logo {
        width: 55px;
        height: 55px;
    }
    #nav a {
        color: #ffffff;  
        text-decoration: none;     
        margin: 10px;        
        transition: .5;
    }
    #nav a:hover {
        color: #E4700C;
    }

    #nav a:active {
        color: #E4700C
    }
</style>