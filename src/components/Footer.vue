<template>
    <div class="footer">
        Developed with <img src="@/assets/vue.png" alt="vuejs" width="14" height="14"/> <img src="@/assets/netlify.png" alt="vuejs" width="14" height="14"/> by <a href="https://rohit.nl" target="_blank">Rohit</a>. 
    </div>
</template>

<script>
export default {
    name: "Footer"
}
</script>

<style scoped>
    .footer {
        background-color: #fff;
        color: #283747;
        text-align: center;
        padding: 1px;
        font-size: 18px;
    }

    .footer span {
        color: #db0000;
    }

    .footer a:link, a:visited {
        color: #283747;
        text-decoration: none;
    }
</style>