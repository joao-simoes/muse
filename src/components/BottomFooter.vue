<template>
    <div class="jsfooter">
        <div class="row text-center">
            <a href="https://www.buymeacoffee.com/jsimoes"><img
                    src="https://img.buymeacoffee.com/button-api/?text=Buy me a beer&emoji=🍺&slug=jsimoes&button_colour=6F00DD&font_colour=000000&font_family=Poppins&outline_colour=000000&coffee_colour=FFDD00" /></a>
        </div>
        <div class="row text-center">
            <p class="my-4">
                All Rights Reserved ©
                <a href="https://www.joao-simoes.pt" target="_blank"><b>João Simões</b></a>, {{ year }}
            </p>
        </div>
    </div>
</template>
<script>
export default {
    name: "BottomFooter",
    data() {
        return {
            year: 2022,
        };
    },
    mounted() {
        const today = new Date();
        this.year = today.getFullYear();
    },
};
</script>

<style scoped>
a {
    color: rgba(127, 17, 224, 1);
    text-decoration: none;
}

p {
    line-height: 10px;
}

.jsfooter {
    margin: 0 auto;
    border-top: 1px solid rgba(127, 17, 224, 0.25);
    transition: ease-in-out 0.2s;
}

.jsfooter a:hover {
    font-size: 18px;
    transition: ease-in-out 0.2s;
}
</style>