<template>
    <div class="container">
        <div class="card">
            <img src="../assets/img/bg.jpg" class="card-img-top">
            <div class="card-body">
                <p class="card-text">
                    <ul>
                        <li class="p-3 mb-2 bg-light text-dark" v-for="item in music" :key="item.id">
                            <div class="text">
                                <span>
                                    {{ item.desc }}
                                </span>
                            </div>
                            <div class="icon" @click="select(item.id)">
                                <template v-if="item.id === id">
                                    <img width="24" src="../assets/img/pause.svg" @click="musicStop()">
                                </template>
                                <template v-else>
                                    <img width="24" src="../assets/img/play.svg" @click="musicPlay(item.src)">
                                </template>
                            </div>
                        </li>
                    </ul>
                </p>
            </div>
        </div>
    </div>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue';
import Music from '@/types/Create';

import mp1 from '../assets/music/1.mp3';
import mp2 from '../assets/music/2.mp3';
import mp3 from '../assets/music/3.mp3';

export default defineComponent({
    name: 'Home',
    setup() {
        let id = ref <number> (0);

        const music = ref <Music[]> ([
            { id: 1, src: mp1, desc: 'Escape & Даня Милохин - so low' },
            { id: 2, src: mp2, desc: 'Kambulat - она немного ниже меня ростом'},
            { id: 3, src: mp3, desc: 'Егор Натс – Ты красивая, как осень' },
        ])

        const select = (idMusic: number) => {
            id.value = idMusic
        }

        let audio: HTMLAudioElement;

        const musicPlay = (sl: string) => {

            if (audio) {
              audio.pause();
              audio.currentTime = 0
            }

            audio = new Audio(sl);
            audio.play()
        }

        const musicStop = () => {
            id.value = 0;
            audio.pause();
            audio.currentTime = 0
        }

        return { id, music, select, musicPlay, musicStop }
    }
});
</script>

<style>
.container {
    width: 95%;
    height: 100vh;
    display: flex;
    justify-content: center;
}

.card-body,
ul {
    padding: 0;
}

.icon {
  background: #dbe4ed;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 32px;
}

li {
    position: inherit;
    display: flex;
    justify-content: space-between;
    overflow: hidden;
    white-space: nowrap;
}

.text {
  width: 67px;
  animation: 14s linear 0s infinite alternate change;
}

@keyframes change {
    from {
        margin-left: 10%;
    }

    to {
        margin-left: -100%;
    }
}
</style>