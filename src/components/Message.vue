<template>
    <div class="message-container">
        <p>{{msg}}</p>
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
    .message-container{
        color: #fff;
        background-color: #22ad68;
        border: 1px solid #22ad68;
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
    }

</style>