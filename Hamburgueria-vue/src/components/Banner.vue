<template>
    <div id="main-banner">
        <div id="textos">
            <h1>LYNCAS</h1>
            <h2> BURGUERIA HOUSE</h2>
            <h3>- BEST BURGER -</h3>
            <button id="botao-main">Fazer Pedido</button>
        </div>
    </div>
</template>

<script>
export default {
    name: "Banner"
}
</script>

<style scoped>
    #main-banner {  
        margin-top: -81px;
        height: 800px;  
        background-image: url('/public/img/burger.jpg');             
        display: grid;
        align-items: center;
        justify-content: right;
    }

    #textos h1 {
    color: #f7f7f7;
    text-shadow: #000000fd 2px 2px 5px;
    font-size: 100px;
    width: 700px;
    margin-right: 300px;
    text-align: center;
    line-height: 1em;
  }

  #textos h2 {
    color: #f7f7f7;
    text-shadow: #000000fd 2px 2px 5px;
    font-size: 40px;
    margin-right: 300px;
    text-align: center;
    line-height: 1.2em;
  }

  #textos h3 {
    color: #f7f7f7;
    text-shadow: #000000fd 2px 2px 5px;
    font-size: 30px;
    margin-right: 300px;
    text-align: center;
    line-height: 1.8em;
  }
  
  #botao-main{
    padding: 15px 40px;
    margin-top: 16px;
    margin-left: 240px;
    border-radius: 100px;
    background-color: #E4700C;
    color: #f7f7f7;
    font-weight: bold;
    font-size: 20px;
    line-height: 1em;
    cursor: pointer;
  }
  #botao-main:hover {
    z-index: -1;
    background-color: #f7f7f7;
    color: #E4700C;
    transition: all 0.3s;
  }
</style>