<script>
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

  setInterval(() => {
    changeColor()
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

<div class="container" on:click={changeColor} style="background: {bgColor}">
  <h1 style="color: white">taptone</h1>
</div>
