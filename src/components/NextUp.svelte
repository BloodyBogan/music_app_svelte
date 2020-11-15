<script>
    export let nextSongTitle;
    export let nextSongArtist;
</script>

<div class="next-up">
    <p>Next up: <span>{nextSongTitle} by {nextSongArtist}</span></p>
</div>

<style lang="scss">
    .next-up {
        p {
            font-size: 1.6rem;
            font-weight: 500;
            text-align: center;
            color: #888;

            span {
                font-weight: 400;
                font-style: italic;
            }
        }
    }
</style>