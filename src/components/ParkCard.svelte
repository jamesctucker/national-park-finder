<script>
    export let park;
</script>

<div class="card">
    <img src={park.images[0].url} alt="photo of national park" class="park-image">
        <h1 class="title">{park.fullName}</h1>
</div>

<style>
    .card {
        background: white;
        filter: drop-shadow(10px 5px 8px lightgray);
        max-width: 300px;
        margin: 2rem;
        position: relative;
    }

    .card:hover {
        transform: scale(1.1);
    }

    .title {
        padding: 1rem;
    }


    .park-image {
        height: 60%;
        width: 100%;
    }
</style>