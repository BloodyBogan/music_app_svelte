<script>
    import { onDestroy } from 'svelte';

    import { songsStore } from '../store.js'

    import SongInfo from './SongInfo.svelte';
    import Controls from './Controls.svelte';
    import NextUp from './NextUp.svelte';

    let songs;

    const unsubscribe = songsStore.subscribe(value => songs = value);

    let audioElement;

    let currentSongIndex;
    let nextSongIndex;

    let songTitle;
    let songArtist;
    let songImageUrl;
    let songPath;

    let nextSongTitle;
    let nextSongArtist;

    let paused = true;
    let ended = false;

    $: if(ended) {
        changeSong();
    }

    const initPlayer = () => {
        currentSongIndex = 0;
        nextSongIndex = currentSongIndex + 1;
        
        updatePlayer();
    }

    const updatePlayer = () => {
        let song = songs[currentSongIndex];

        songTitle = song.title;
        songArtist = song.artist;
        songImageUrl = song.imagePath;

        nextSongTitle = songs[nextSongIndex].title;
        nextSongArtist = songs[nextSongIndex].artist;

        songPath = song.songPath;
    }

    const togglePlaySong = () => {
        if (audioElement) {
            if (paused) {
                audioElement.play();
            } else {
                audioElement.pause();
            }
        }
    }

    const changeSong = async (next = true) => {
        if (next) {
            currentSongIndex++;
            nextSongIndex = currentSongIndex + 1;

            if (currentSongIndex > songs.length - 1) {
                currentSongIndex = 0;
                nextSongIndex = currentSongIndex + 1;
            }

            if (nextSongIndex > songs.length - 1) {
                nextSongIndex = 0;
            }
        } else {
            currentSongIndex--;
            nextSongIndex = currentSongIndex + 1;

            if (currentSongIndex < 0) {
                currentSongIndex = songs.length - 1;
                nextSongIndex = 0;
            }
        }

        updatePlayer();

        await audioElement.load();

        if(!paused) {
            audioElement.play();

            return;
        }

        audioElement.pause();
    }

    initPlayer();

    onDestroy(unsubscribe);
</script>

<section class="player">
    <audio bind:this={audioElement} bind:paused bind:ended>
        <source src={songPath} on:error={() => location.reload()}>
        <p>
            Your browser doesn't support HTML5 audio.
        </p>
    </audio>
    <SongInfo {songTitle} {songArtist} {songImageUrl} {paused} />
    <Controls on:playClick={togglePlaySong} on:previousClick={() => changeSong(false)} on:nextClick={changeSong} {paused} />
    <NextUp {nextSongTitle} {nextSongArtist} />
</section>

<style lang="scss">
    .player {
        max-width: 100%;
        width: 41.4rem;
        padding: 10rem 5rem;
        background-color: #fff;
        border-radius: 1.6rem;
        box-shadow: 0 0.3rem 1.2rem rgba(0, 0, 0, 0.1);
    }

    @media (max-width: 414px) {
        .player {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            border-radius: 0;
            padding: 7.5rem 3rem;
        }
    }
</style>