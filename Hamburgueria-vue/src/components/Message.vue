<template>
    <div class="message-container">
        <p>{{ msg }}</p>
    </div>
    
</template>

<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container {
        color: #E4700C;
        background-color: #e4710c1e;
        border: 2px solid #E4700C;
        border-radius: 8px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
        text-align: center;
    }
</style>