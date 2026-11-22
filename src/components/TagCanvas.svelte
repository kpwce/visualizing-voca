<script>
  import { onMount } from 'svelte';

  let canvas;

  onMount(() => {
    const ctx = canvas.getContext('2d');
    let animationFrameId;
    let isDestroyed = false;

    function handleResize() {
      if (!canvas) return;
      canvas.width = canvas.clientWidth;
      canvas.height = canvas.clientHeight;
    }

    handleResize();
    window.addEventListener('resize', handleResize);

    async function init() {
      try {
        const response = await fetch('/visualization_data/reading_tag_counts.json');
        const countsDict = await response.json();

        if (isDestroyed) return;

        const freqs = Object.values(countsDict);
        const maxFreq = Math.max(...freqs);

        const words = Object.entries(countsDict).map(([text, freq]) => {
          const brightness = 0.2 + (freq / maxFreq) * 0.8;
          return {
            text,
            brightness,
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            speed: 0.1 + Math.random(),
          };
        });

        function loop() {
          if (isDestroyed) return;

          ctx.clearRect(0, 0, canvas.width, canvas.height);
          ctx.font = '18px serif';

          for (const w of words) {
            w.x -= w.speed;
            const textWidth = ctx.measureText(w.text).width;

            if (w.x < -textWidth) {
              w.x = canvas.width;
            }

            ctx.fillStyle = `rgba(255, 255, 255, ${w.brightness})`;
            ctx.fillText(w.text, w.x, w.y);
          }

          animationFrameId = requestAnimationFrame(loop);
        }

        loop();
      } catch (error) {
        console.error("Tags didn't load: ", error);
      }
    }

    init();

return () => {
      isDestroyed = true;
      window.removeEventListener('resize', handleResize);
      if (animationFrameId) cancelAnimationFrame(animationFrameId);
    };
  });
</script>

<canvas bind:this={canvas} id="animated-tags"></canvas>

<style>
  canvas {
    grid-area: 1 / 1;
    display: block;
    width: 100%;
    height: 100%;
    background: black;
    pointer-events: none;
    z-index: 0;
  }
</style>