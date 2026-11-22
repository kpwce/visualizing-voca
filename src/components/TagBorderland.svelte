<script>
  let borderlandsText = 'Try to categorize the "borderlands" tag.';

  function showUSLocationsText() {
    borderlandsText = 'Clicked US Locations';
  }

  function showWorldLocationsText() {
    borderlandsText = 'Clicked World Locations';
  }

  function showIdentityText() {
    borderlandsText = 'Clicked Identity';
  }

  function showNewCategory() {
    borderlandsText = 'Clicked None of the above';
  }
</script>

<div class="borderlands-content">

  <p id="borderlands-text">{borderlandsText}</p>

  <button class="borderlands-button" on:click={showUSLocationsText}>
    Locations: United States
  </button>
  <button class="borderlands-button" on:click={showWorldLocationsText}>
    Locations: World
  </button>
  <button class="borderlands-button" on:click={showIdentityText}>
    Identity
  </button>
  <button class="borderlands-button" on:click={showNewCategory}>
    New Category
  </button>

  <p>Wow, that was complicated! And that's just one tag!</p>
</div>

<style>
    button {
        color: black;
        background-color: rgb(170, 124, 84);
        font-family: 'Courier New', Courier, monospace;
        font-weight: bold;
        border-style: none;
        padding: 20px;
        margin: 10px;
        border-radius: 5px;

    }

    button:hover {
        background-color: rgb(126, 86, 50);
    }

    #borderlands-text {
        border-color: black;
        border-style: double;
        border-radius: 5px;
    }
</style>