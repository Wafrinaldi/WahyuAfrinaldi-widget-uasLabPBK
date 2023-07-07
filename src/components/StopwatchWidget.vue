<template>
    <div class="stopwatch-widget">
        <h2 class="widget-title">Stopwatch Widget</h2>
        <p class="stopwatch-time">{{ formatTime(stopwatchTime) }}</p>
        <div class="stopwatch-controls">
            <button @click="startStopwatch" :disabled="isRunning">Start</button>
            <button @click="pauseStopwatch" :disabled="!isRunning">Pause</button>
            <button @click="resetStopwatch" :disabled="!stopwatchTime">Reset</button>
        </div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            stopwatchTime: 0,
            isRunning: false,
            stopwatchInterval: null
        };
    },
    methods: {
        startStopwatch() {
            if (!this.isRunning) {
                this.stopwatchInterval = setInterval(() => {
                    this.stopwatchTime += 0.01;
                }, 10);
                this.isRunning = true;
            }
        },
        pauseStopwatch() {
            if (this.isRunning) {
                clearInterval(this.stopwatchInterval);
                this.isRunning = false;
            }
        },
        resetStopwatch() {
            this.stopwatchTime = 0;
            this.isRunning = false;
            clearInterval(this.stopwatchInterval);
        },
        formatTime(time) {
            const minutes = Math.floor(time / 60)
                .toString()
                .padStart(2, '0');
            const seconds = Math.floor(time % 60)
                .toString()
                .padStart(2, '0');
            const milliseconds = Math.floor((time % 1) * 100)
                .toString()
                .padStart(2, '0');
            return `${minutes}:${seconds}.${milliseconds}`;
        }
    }
};
</script>
  
<style scoped>
.stopwatch-widget {
    padding: 20px;
    margin: 100px auto;
    height: 23vh;
    width: 40%;
    text-align: center;
    background-color: rgba(255, 255, 255, 0.2);
    box-shadow: 0px 0px 8px 3px #888888;
    text-align: center;
}

.widget-title {
    margin-top: 0;
    font-size: 30px;
    margin-top: 15px;
    font-weight: 300;
    color: #fff;
}

.stopwatch-time {
    font-size: 36px;
    margin-bottom: 10px;
}

.stopwatch-controls {
    display: flex;
    justify-content: center;
}

button {
    padding: 8px 12px;
    border: none;
    background-color: #fa8072;
    color: #fff;
    font-size: 16px;
    font-weight: bold;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
    margin: 0 5px;
}

button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
}
</style>
  