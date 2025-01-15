<script>
    import { onMount } from 'svelte';

    let helloString = '';
    let isHello = true;

    function updateString() {
        const word = 'hello ';
        const repetitions = Math.ceil(window.innerWidth * window.innerHeight / (word.length * 25));
        helloString = word.repeat(repetitions).trim();
        if (!isHello) {
            const helloIndices = [];
            let index = helloString.indexOf('hello');
            while (index !== -1) {
                helloIndices.push(index);
                index = helloString.indexOf('hello', index + 1);
            }
            if (helloIndices.length > 0) {
                const randomIndex = helloIndices[Math.floor(Math.random() * helloIndices.length)];
                helloString = helloString.substring(0, randomIndex) + 'hell' + helloString.substring(randomIndex + 'hello'.length);
            }
        }
        isHello = !isHello;
    }

    onMount(() => {
        updateString();
        setInterval(updateString, 2000);
    });
</script>

<svg>
    <defs>
        <filter id="distortLow">
            <feTurbulence baseFrequency="0.01 0.01" numOctaves="1" result="noise" />
            <feDisplacementMap in="SourceGraphic" in2="noise" scale="5" xChannelSelector="R" yChannelSelector="R">
        </filter>
    </defs>
</svg>

<svg>
    <defs>
        <filter id="distort">
            <feTurbulence baseFrequency="0.01 0.01" numOctaves="1" result="noise"  />
            <feDisplacementMap in="SourceGraphic" in2="noise" scale="10" xChannelSelector="R" yChannelSelector="R">
        </filter>
    </defs>
</svg>

<main data-content={helloString}>
    <a href="/home">enter</a>
</main>


<style>

    svg{
        display: none;
    }

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
        filter: url(#distortLow);
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

    a{
        padding: 2rem 10rem;
        filter: url(#distort);
        font-size: 2rem;
        font-family: "Special Elite", serif;
        text-decoration: none;
        background-color: white;
        color: black;
    }

    a:hover{
        animation-name: shake;
        animation-duration: 50ms;
        animation-iteration-count: infinite;
        animation-timing-function: linear;
    }

    @keyframes shake{
        0%{
            transform: translate(0.1rem, -0.1rem);
        }

        50%{
            transform: translate(-0.1rem, 0.1rem);
        }

        100%{
            transform: translate(0.1rem, -0.1rem);
        }
    }

</style>