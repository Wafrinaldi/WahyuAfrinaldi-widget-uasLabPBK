<template>
    <div id="vue-app">
        <h2>Punch Game</h2>
        <!-- bag image -->
        <div id="bag" v-bind:class="{ burst: ended }"></div>

        <!-- bag health -->
        <div id="bag-health">
            <div v-bind:style="{ width: health + '%' }"></div>
        </div>

        <!-- game control -->
        <div id="controls">
            <button v-on:click="punch" v-show="!ended">Punch</button>
            <button v-on:click="restart">Restart</button>
        </div>
    </div>
</template>
  
<script>
export default {
    name: "#vue-app",
    data() {
        return {
            health: 100,
            ended: false
        };
    },
    methods: {
        punch() {
            this.health -= 10;
            if (this.health <= 0) {
                this.ended = true;
            }
        },
        restart() {
            this.health = 100;
            this.ended = false;
        }
    }
};
</script>
  
<style>
body {
    background-color: #000;
    color: white;
    margin: 0;
    padding: 0;
}

#bag {
    height: 50vh;
    width: 500px;
    margin: 0 auto;
    background: url(../assets/bag.jpeg) center no-repeat;
    background-size: 80%;
}

#bag.burst {
    background: url(../assets/bag-burst.jpeg) center no-repeat;
    background-size: 80%;
}

#bag-health {
    width: 200px;
    border: 2px solid #000;
    margin: 0 auto 20px auto;
}

#bag-health div {
    height: 20px;
    background: crimson;
}

#controls {
    width: 200px;
    margin: 0 auto;
}

h2 {
    margin-top: 50px;
    font-size: 30px;
    font-weight: 300;
}

button {
    padding: 8px 12px;
    border: none;
    display: inline-block;
    background-color: #fa8072;
    color: #fff;
    font-size: 16px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    margin-right: 20px;
}

button:hover {
    background-color: #fa8090;
}
</style>
  