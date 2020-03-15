<template>
    <main class="main">
        <button
            class="startBtn"
            @click="appStart"
            v-if="isStarted==false"
            >
            Start
        </button>
        <section
            @mousedown="ringStart"
            @touchstart="ringStart"
            @mouseup="ringStop"
            @touchend="ringStop"
            @mouseleave="ringStop"
            @touchleave="ringStop"
            @mousemove="ring"
            @touchmove="ring"
            class="touchZone"
            v-else
            >
        </section>
    </main>
</template>

<script>
import Tone from 'tone'
export default {
    data() {
        return {
            isStarted: false,
            snyth: null,
            isRing: false
        }
    },
    methods: {
        appStart(){
            this.isStarted = true
            this.synth = new Tone.MonoSynth().toMaster();
        },
        musicStart() {
            var synth = new Tone.Synth().toMaster()
            synth.triggerAttackRelease('C4', '8n')
        },
        ringStart() {
            this.isRing = true;
            this.ring()
        },
        ringStop() {
            this.isRing = false;
            this.ring()
        },
        ring() {
            if(this.isRing) {
                this.synth.triggerAttack('C3');
            } else {
                this.synth.triggerRelease();
            }
        }
    }
}
</script>

<style scoped>
.main{
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
.startBtn{
    padding: 10px 20px;
}
.touchZone{
    background: linear-gradient( 45deg, rgb(255,255,255), rgb(100,255,255));
    width: 100%;
    min-width: 100%;
    height: 100vh;
    min-height: 100vh;
}
</style>