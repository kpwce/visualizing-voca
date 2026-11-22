    <style>

        #scroll {
            position: relative;
            display: block; 
            width: 100%;
            padding: 0;
            margin-top: 2rem;
            flex-direction: column;
        }

        .scroll__graphic {
            position: -webkit-sticky;
            position: sticky;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh; 
            z-index: 0;
        }

        .chart {
            position: absolute;
            top: 100px;
            width: 100%;
        }

        .scroll__text {
            position: relative;
            width: 100%;
            max-width: 500px;
            margin: 0 auto; 
            padding: 50vh 1rem 0 1rem;
            z-index: 1; 
        }

        .step {
            margin: 0 auto 70vh auto; 
            padding: 1.5rem;
            background-color: rgba(255, 255, 255, 0.98); 
            border: 2px solid #202124;
            border-radius: 8px;
            opacity: 0; 
            transition: opacity 150ms ease-in-out;
            pointer-events: none; 
        }

        .step.is-active {
            opacity: 1;
            pointer-events: auto;
        }

        .step:last-child {
            margin-bottom: 70vh; 
        }

        .step p {
            font-size: 1.25rem;
            margin: 0;
        }



	.scroll__graphic {
		height: 45dvh;
		max-height: 45dvh;
		z-index: 1;
		background: rgba(255, 255, 255, 0.96);
	}

	.chart,
	.chart :global(svg) {
		max-height: 40dvh;
	}

	.scroll__text {
		z-index: 2;
		pointer-events: none;
	}

	.step {
		pointer-events: auto;
		box-shadow: 0 4px 20px rgba(0, 0, 0, 0.12);
	}

    </style>
<script>
import { onMount } from "svelte";
import * as d3 from "d3";
import cloudModule from "d3-cloud";
import scrollama from "scrollama";

const cloud = cloudModule.default ?? cloudModule;

	// --- Scrollytelling State & Refs ---
	let scrollContainer;
	let graphicEl;
	let chartEl;
	let activeStep = $state(0);

	const steps = [
		{
			html: `Consider this Spring 2025 reading from American poet and educator Terrance Hayes, which can be found <a href="https://voca.arizona.edu/reading/terrance-hayes-february-13-2025">here</a>.`,
		},
		{
			html: `Poetry readings are more than just poetry. They often begin with an introduction to the reading.`,
		},
		{
			html: `Readers also can give commentary about their work to enrich how the audience experiences a poem.`,
		},
		{
			html: `But at the heart of the reading are the poems.`,
		},
		{
			html: `Some were published long ago. Some were published recently. Some were unpublished at the time, or uncollected. To explore the uncollected, take a look at <a href="./visualizing-voca/understanding-the-uncollected" class="internal-link">Understanding the Uncollected</a>.`,
		},
		{
			html: `The poems and themes from one reading are put into conversation with other readings in Voca through subject tags. To explore tags in depth, take a look at <a href="./visualizing-voca/tumultuous-tags" class="internal-link">Tumultuous Tags</a>.`,
		},
		{
			html: `Sometimes moderators or the live audience get to ask questions after a reading. But what about those watching online? See <a href="./visualizing-voca/making-metapoetry" class="internal-link">Making Metapoetry</a> for some ideas on how to actively participate in these poetic conversations.`,
		},
	];

	const colorMap = {
		Introduction: "#E07A5F",
		Commentary: "#457B6D",
		Poem: "#3D405B",
		"Q&A": "#D4A373",
	};


	onMount(() => {
		let svg, rectangles, rectangleLabels;
		const scroller = scrollama();

		function handleResize() {
			if (!chartEl || !graphicEl) return;
			const figureHeight = window.innerHeight / 2;
			chartEl.style.height = `${figureHeight}px`;
			graphicEl.style.height = `${window.innerHeight}px`;

			if (svg) {
				const chartWidth = chartEl.clientWidth;
				svg.attr("width", chartWidth)
					.attr("height", figureHeight)
					.style("overflow", "visible");
			}

			scroller.resize();
		}

		function handleStepEnter(response) {
			activeStep = response.index;

			const enabledType = new Set();
			if (response.index >= 1) enabledType.add("Introduction");
			if (response.index >= 2) enabledType.add("Commentary");
			if (response.index >= 3) enabledType.add("Poem");
			if (response.index >= 6) enabledType.add("Q&A");

			if (rectangles) {
				rectangles
					.transition()
					.duration(300)
					.attr("fill", (d) =>
						enabledType.has(d.Type) ? colorMap[d.Type] : "#d3d3d3"
					);
			}

			if (rectangleLabels) {
				rectangleLabels
					.transition()
					.duration(300)
					.text((d) => {
						if (response.index === 4) return d.Published;
						if (response.index === 5) return d.Tags;
						return d.Track;
					});
			}
		}

		svg = d3.select(chartEl).append("svg");

		d3.csv("./visualizing-voca/visualization_data/terrance_hayes.csv").then((data) => {
			const squareSize = 24;
			const gap = 4;

			rectangles = svg
				.selectAll("rect")
				.data(data)
				.join("rect")
				.attr("width", squareSize)
				.attr("height", squareSize)
				.attr("x", 5)
				.attr("y", (d, i) => i * (squareSize + gap))
				.attr("fill", "#d3d3d3")
				.attr("rx", 4);

			rectangleLabels = svg
				.selectAll("text.label")
				.data(data)
				.join("text")
				.attr("class", "label")
				.attr("x", 10 + squareSize)
				.attr("y", (d, i) => i * (squareSize + gap) + squareSize / 2)
				.attr("text-anchor", "start")
				.attr("dominant-baseline", "central")
				.attr("fill", "#202124")
				.style(
					"font-family",
					"Baskerville, Georgia, Times, 'Times New Roman', serif"
				)
				.style("font-size", "13px")
				.text((d) => d.Track);

			scroller
				.setup({
					step: ".scroll__text .step",
					offset: 0.7,
					debug: false,
				})
				.onStepEnter(handleStepEnter);

			handleResize();
		});
	});
</script>

<div id="readings-chart"></div>

<section id="scroll" bind:this={scrollContainer}>
	<div class="scroll__graphic" bind:this={graphicEl}>
		<div class="chart" bind:this={chartEl}></div>
	</div>

	<div class="scroll__text">
		{#each steps as step, i}
			<div
				class="step"
				class:is-active={activeStep === i}
				data-step={i}
			>
				<p>{@html step.html}</p>
			</div>
		{/each}
	</div>
</section>
