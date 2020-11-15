<script>
    export let paused;
    export let songTitle;
    export let songArtist;
    export let songImageUrl;
</script>

<div class="song-image {paused ? '' : 'pulse-animation'}" style="background-image: url('{songImageUrl}')"></div>
<div class="song-details">
    <h2>{songTitle}</h2>
    <h3>{songArtist}</h3>
</div>

<style lang="scss">
    .song-image {
        position: relative;
        display: block;
        max-width: 100%;
        width: 20rem;
        margin: 0 auto 5rem auto;
        background-color: #fff;
        background-repeat: no-repeat;
        background-position: center;
        background-size: cover;
        border-radius: 50%;
        box-shadow: 0 0.3rem 1.2rem rgba(0, 0, 0, 0.3);
        transition-property: background-image;
        transition-duration: 0.4s;
        transition-timing-function: ease;

        &::before {
            content: '';
            position: absolute;
            display: block;
            top: -2rem;
            left: -2rem;
            right: -2rem;
            bottom: -2rem;
            border: 0.2rem solid #eee;
            border-radius: 50%;
        }

        &::after {
            content: '';
            display: block;
            padding-top: 100%;
        }

        &.pulse-animation {
            animation: pulse 2s infinite; 
        }
    }

    .song-details {
        margin-bottom: 3rem;
        text-align: center;

        h2 {
            margin-bottom: 0.5rem;
            font-size: 2.4rem;
            font-weight: 600;
            line-height: 1.25;
            color: #313131;
        }

        h3 {
            font-size: 1.6rem;
            font-weight: 500;
            color: #888;
        }
    }

    @keyframes pulse {
        from {
            box-shadow: 0 0 0 0 rgba(0, 0, 0, 0.3);
        }

        to {
            box-shadow: 0 0 0 2rem rgba(0, 0, 0, 0);
        }
    }
</style>