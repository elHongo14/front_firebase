<template>
    <div class="bg">
        <v-row class="renglon">
            <nuxt />
        </v-row>
    </div>
</template>

<style scoped>
.bg {
    background: url('../assets/images/bg.png');
    background-size: cover;
    height: 100vh;
    width: 100vw;
}
.renglon {
    padding: 150px;
    flex-direction: row;
    align-content: center;
    justify-content: center;
    align-items: center;
}
</style>