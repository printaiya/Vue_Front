<template>
    <div class="wrapper">
        <main_page></main_page>
    </div>
</template>
<script>
import main_page from '@/components/main.vue'
export default {
    name: "App",
    components: {
        main_page
    }
}
</script>
<style>
*, *::after, *::before {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-size: 25px;
    color: #000;
    list-style: none;
    font-weight: 100;
}
button {
    padding: 5px 0px;
    margin: 5px;
    width: 70px;
    text-align: center;
}
input {
    padding: 5px;
    margin-top: 10px;
}
button:hover {
    cursor: pointer;
}
</style>