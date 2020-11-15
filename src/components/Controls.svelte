<script>
    export let paused;

    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();

    const handleClickPlay = () => {
        dispatch('playClick');
    }

    const handleClickPrevious = () => {
        dispatch('previousClick');
    }

    const handleClickNext = () => {
        dispatch('nextClick');
    }
</script>

<div class="controls">
    <button class="controls__skip" on:click={handleClickPrevious}>
        <i class="fas fa-backward fa-lg"></i>
    </button>
    <button class="controls__play" on:click={handleClickPlay}>
        <i class="fas {paused ? 'fa-play' : 'fa-pause'} fa-2x"></i>
    </button>
    <button class="controls__skip" on:click={handleClickNext}>
        <i class="fas fa-forward fa-lg"></i>
    </button>
</div>

<style lang="scss">
    .controls {
        display: flex;
        align-items: center;
        justify-content: center;
        margin-bottom: 3rem;

        button {
            border: none;
            outline: none;
            appearance: none;
            transition-duration: 0.25s;
            transition-timing-function: ease;
            cursor: pointer;
        }

        &__play {
            width: 7.5rem;
            height: 7.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 2rem;
            color: #fff;
            background-color: #fe4880;
            border-radius: 50%;
            box-shadow: 0 0.6rem 1.2rem rgba(254, 72, 128, 0.6);
            transition-property: box-shadow;

            &:hover, &:focus {
                box-shadow: 0 0.8rem 1.6rem rgba(254, 72, 128, 0.8);
            }

            &:active {
                transform: scale(0.98);
                box-shadow: 0 0.4rem 0.8rem rgba(254, 72, 128, 0.8);
            }
        }

        &__skip {
            padding: 1rem;
            color: #ccc;
            background: none;
            transition-property: color;

            &:hover, &:focus {
                color: #888;
            }
        }
    }
</style>