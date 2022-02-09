<template>
    <footer>
        <p>The Botaminder Project by Team FreshBOTS</p>
            <a href="https://github.com/mostlyaman/botaminder" target="_blank">
            <w-button bg-color = "black" color = 'white' lg>
            <i class="fa-brands fa-github-square fa-1x"></i>Github
            </w-button>
            </a>
    </footer>
</template>

<script>
export default {
    name: 'Footer'
}
</script>

<style scoped>
footer {
    padding: 20px;
}
p {
    padding:20px;
}

h4 {
    text-align: center;
}

.fa-brands {
    size: 20px;
    padding-right: 10px;
}

</style>