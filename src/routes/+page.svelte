<script>
    import { onMount } from 'svelte';

    let helloString = '';

    onMount(() => {
        const hello = 'hello ';
        const repetitions = Math.ceil(window.innerWidth * window.innerHeight / (hello.length * 25));
        helloString = hello.repeat(repetitions).trim();
    });
</script>

<main data-content={helloString}>
    <button>button 1</button>
    <button>button 2</button>
    <button>button 3</button>
</main>


<style>
    main {
        min-height: 100vh;
        min-width: 100vw;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100%;
        width: 100%;
        gap: 5rem 0;
    }

    main::before {
        content: attr(data-content);
        position: absolute;
        z-index: -1;
        color: white;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        overflow: hidden;
        background-image: url("/assets/noise.png");
        background-repeat: no-repeat;
        background-size: cover;
        background-position: center;
        color: transparent;
        background-clip: text;
        filter: invert(1);
    }

    button{
        padding: 2rem 10rem;
    }
</style>