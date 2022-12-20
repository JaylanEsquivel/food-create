<template>
    <nav>
        <routerLink to="/" id="url_logo">
            <img :src="logo" :alt="alt" id="logo" />
        </routerLink>

        <router-link to="/">Home</router-link>
        <router-link to="/pedidos">Pedidos</router-link>
    </nav>
</template>
<script>
    export default {
        name: 'Navbar',
        props: ['logo', 'alt']
     }
</script>
<style scoped>

    nav{
        background-color: #222;
        border-color: #111;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }
    nav a{
        color: #fdfdfd;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }
    nav a:hover{
        color: #ffb900;
    }

    #url_logo{
        margin: auto;
        margin-left: 0;
    }
    #url_logo img{
        width: 40px;
    }

    


</style>