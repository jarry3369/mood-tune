<script>
	import { onMount } from 'svelte'

	let bgColor = getRandomColor()

  function getRandomColor() {
    let h, s, l
	do {
		h = Math.floor(Math.random() * 360)
		s = Math.floor(Math.random() * 101)
		l = Math.floor(Math.random() * 101)
	} while (l < 15 || l > 90 || s < 20)

	return `hsl(${h}, ${s}%, ${l}%)`
  }

  function changeColor() {
    bgColor = getRandomColor()
  }

  function updateFavicon(hsl) {
	const size = 64
	const canvas = document.createElement('canvas')
	canvas.width = canvas.height = size
	const ctx = canvas.getContext('2d')
	if (!ctx) return

	ctx.fillStyle = hsl
	ctx.fillRect(0, 0, size, size)

	const url = canvas.toDataURL('image/png')
	const link = document.querySelector("link[rel~='icon']") || document.createElement('link')
	link.rel = 'icon'
	link.href = url
	document.head.appendChild(link)
	}

	onMount(()=>{
		updateFavicon(bgColor)
	})

  	setInterval(() => {
		changeColor()
		updateFavicon(bgColor)
	}, 6000)
</script>

<style>
  :global(html, body) {
    margin: 0;
    padding: 0;
    height: 100%;
    width: 100%;
  }

  :global(*) {
    box-sizing: border-box;
  }

  .container {
	will-change: background;
    width: 100vw;
    height: 100vh;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: background 1s;
    user-select: none;
    cursor: pointer;
  }

  h1 {
    font-size: 6rem;
    font-weight: 900;
    margin: 0;
    padding: 0;
  }
</style>

<svelte:head>
  <title>taptone</title>
  <meta name="description" content="mind reset with taptone" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <meta property="og:title" content="taptone" />
  <meta property="og:description" content="mind reset with taptone" />
  <meta property="og:type" content="website" />
  <meta property="og:url" content="https://taptone.vercel.app/" />
</svelte:head>

<div class="container" on:click={changeColor} style="background: {bgColor}">
  <h1 style="color: white">taptone</h1>
</div>
