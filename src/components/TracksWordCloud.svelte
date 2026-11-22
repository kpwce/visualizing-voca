<script>
	import { onMount } from "svelte";
	import * as d3 from "d3";
	import cloudModule from "d3-cloud";

	const cloud = cloudModule.default ?? cloudModule;

	let cloudWrapperEl;
	let wordcloudSvgEl;
	let words = [];
	let selectedWord = $state(null);
	let searchQuery = $state("");

	const cloudColors = [
		"#202124",
		"#3D405B",
		"#E07A5F",
		"#457B6D",
		"#6D597A",
		"#D4A373",
	];

	let filteredTracks = $derived.by(() => {
		if (!selectedWord) return [];
		const q = searchQuery.trim().toLowerCase();
		if (!q) return selectedWord.tracks;

		return selectedWord.tracks.filter((track) => {
			const reading = (track.reading_title || "").toLowerCase();
			const name = (track.track_name || "").toLowerCase();
			const other = (track.other_classification || "").toLowerCase();
			return reading.includes(q) || name.includes(q) || other.includes(q);
		});
	});

	onMount(() => {
		function drawCloud() {
			if (!cloudWrapperEl || !wordcloudSvgEl || words.length === 0) return;

			const width = Math.max(
				250,
				Math.floor(cloudWrapperEl.clientWidth - 30)
			);
			const height = 400;

			const maxCount = Math.max(1, ...words.map((w) => w.tracks.length));
			const maxFontSize = Math.min(84, Math.floor(width / 6));
			const sizeScale = d3
				.scaleSqrt()
				.domain([1, maxCount])
				.range([18, maxFontSize]);

			const wordcloudsvg = d3.select(wordcloudSvgEl);
			wordcloudsvg
				.attr("width", width)
				.attr("height", height)
				.attr("viewBox", `0 0 ${width} ${height}`);
			wordcloudsvg.selectAll("*").remove();

			const wordList = words.map((word) => ({
				text: word.text,
				size: sizeScale(word.tracks.length),
				tracks: word.tracks,
			}));

			cloud()
				.size([width, height])
				.words(wordList)
				.padding(3)
				.rotate(() => 0)
				.font("Georgia")
				.fontSize((word) => word.size)
				.on("end", (layoutWords) => {
					wordcloudsvg
						.append("g")
						.attr(
							"transform",
							`translate(${width / 2}, ${height / 2})`
						)
						.selectAll("text")
						.data(layoutWords)
						.join("text")
						.attr("class", "word")
						.attr("text-anchor", "middle")
						.style("cursor", "pointer")
						.style("font-size", (word) => `${word.size}px`)
						.style(
							"fill",
							(word, i) => cloudColors[i % cloudColors.length]
						)
						.attr(
							"transform",
							(word) =>
								`translate(${word.x}, ${word.y}) rotate(${word.rotate})`
						)
						.text((word) => word.text)
						.on("click", (event, d) => {
							const target = d && d.tracks ? d : event;
							selectedWord = target;
							searchQuery = "";
						});
				})
				.start();
		}

		fetch("./visualizing-voca/wordcloud_data.json")
			.then((response) => {
				if (!response.ok) throw new Error("JSON file not loading!");
				return response.json();
			})
			.then((data) => {
				words = Object.entries(data).map(([text, tracks]) => ({
					text,
					tracks,
				}));
				drawCloud();
			})
			.catch((error) => console.error("Wordcloud error: " + error));

		window.addEventListener("resize", drawCloud);

		return () => {
			window.removeEventListener("resize", drawCloud);
		};
	});
</script>

<div class="wordcloud-container">
	<div class="cloud" bind:this={cloudWrapperEl}>
		<svg
			id="word-cloud"
			bind:this={wordcloudSvgEl}
			role="img"
			aria-label="An interactive word cloud of track classifications"
		></svg>
	</div>

	<div class="list">
		<h2 id="heading">
			{#if selectedWord}
				"{selectedWord.text}" occurrences ({selectedWord.tracks.length})
			{/if}
		</h2>

		<input
			id="search"
			bind:value={searchQuery}
			placeholder="Search table for reading, track, or category"
			aria-label="Search words"
		/>

		<div class="scrollable-table">
			<table id="grid">
				<thead>
					<tr>
						<th>Reading</th>
						<th>Track</th>
						<th>More Categories</th>
					</tr>
				</thead>
				<tbody>
					{#if !selectedWord}
						<tr>
							<td colspan="3">Select a word.</td>
						</tr>
					{:else if filteredTracks.length === 0}
						<tr>
							<td colspan="3">No matching tracks found.</td>
						</tr>
					{:else}
						{#each filteredTracks as track}
							<tr>
								<td>
									<a
										href={`https://voca.arizona.edu/${track.reading_link}`}
										target="_blank"
										rel="noopener noreferrer"
									>
										{track.reading_title}
									</a>
								</td>
								<td>
									<a
										href={`https://voca.arizona.edu${track.track_link}`}
										target="_blank"
										rel="noopener noreferrer"
									>
										{track.track_name}
									</a>
								</td>
								<td>
									{track.other_classification ?? ""}
								</td>
							</tr>
						{/each}
					{/if}
				</tbody>
			</table>
		</div>
	</div>
</div>

<style>
	.wordcloud-container {
		display: block;
		gap: 2rem;
		align-items: start;
		margin: 3rem 0;
	}

	.cloud {
		width: 100%;
		min-width: 0;
		border-radius: 8px;
		padding: 1rem;
	}

	#word-cloud {
		width: 100%;
		height: 400px;
		display: block;
	}

	#word-cloud :global(.word) {
		transition: opacity 0.2s ease;
		user-select: none;
	}

	#word-cloud :global(.word:hover) {
		opacity: 0.7;
		text-decoration: underline;
	}

	.list h2 {
		margin-top: 0;
		font-size: 1.25rem;
		min-height: 1.75rem;
	}

	#search {
		width: 100%;
		padding: 0.6rem 0.85rem;
		margin-bottom: 1rem;
		font-size: 0.95rem;
		border: 1px solid #ccc;
		border-radius: 6px;
		box-sizing: border-box;
        font-family: "Baskerville", 'Times New Roman', Times, serif;
	}

	.scrollable-table {
		max-height: 340px;
		overflow-y: auto;
		border: 1px solid #e0e0e0;
		border-radius: 5px;
	}

	#grid {
		width: 100%;
		border-collapse: collapse;
		font-size: 0.92rem;
	}

	#grid thead th {
		position: sticky;
		top: 0;
		background: rgb(215, 215, 215);
		text-align: left;
		padding: 10px;
		z-index: 1;
	}

	#grid tbody td {
		padding: 10px;
		border-bottom: 1px solid #eee;
		vertical-align: top;
        text-align: left;
	}


</style>