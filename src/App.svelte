<script>
  import Loader from "./Loader.svelte";
  import WordData from "./WordData.svelte";

  let word = "";
  let loading = false;
  let wordData = null;

  async function searchWord() {
    if (word.length === 0) {
      return;
    }
    loading = true;
    wordData = null;
    try {
      let res = await fetch(
        "https://api.dictionaryapi.dev/api/v2/entries/en/" + word
      );
      let data = await res.json();
      if (Array.isArray(data)) {
        wordData = data[0];
      } else {
        wordData = "No result";
      }
      loading = false;
    } catch (error) {
      loading = false;
      console.log(error);
    }
  }

  function handleKeyPress(event) {
    if (event.key === "Enter") {
      searchWord();
    }
  }
</script>

<main>
  <div class="header">Dictionary App</div>
  <div class="center">
    <div class="form">
      <div class="form-group">
        <label for="">Search Word</label>
        <span>
          <input
            type="text"
            placeholder="Type a word here"
            bind:value={word}
            on:keyup={handleKeyPress}
          />
          <button id="search-btn" on:click={searchWord}>Search</button>
        </span>
      </div>
    </div>
    {#if loading === true || wordData !== null}
      <div class="result">
        {#if wordData !== null && typeof wordData !== "string"}
          <WordData {wordData} />
        {:else if wordData === null && loading === true}
          <Loader />
        {:else}
          <p class="padding">No result found</p>
        {/if}
      </div>{/if}
  </div>
</main>

<style>
  .header {
    width: 100%;
    padding: 20px;
    background: #111;
    color: #f5f5f5;
    font-size: 20px;
    text-align: center;
  }
  .center {
    margin: 40px auto;
    width: 90%;
    max-width: 90vw;
    background: #444;
  }
  .center,
  .form {
    border-radius: 10px;
  }
  .form {
    background: #ccc;
    padding: 20px;
    border: 1px solid #f5f5f5;
    box-shadow: 0px 0px 5px 2px rgba(255, 255, 255, 0.05);
    margin: 1.25rem 0;
  }
  .form .form-group {
    margin: 10px 0;
  }
  .form .form-group span {
    display: flex;
    gap: 1rem;
  }
  .form .form-group label {
    display: block;
    font-size: 1rem;
    margin-bottom: 0.5rem;
    margin-left: 0.25rem;
  }
  .form .form-group input {
    width: 100%;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #bbb;
    border-radius: 5px;
  }
  .form .form-group button {
    padding: 10px 20px;
    background: #111;
    color: #f5f5f5;
    font-size: 1rem;
    border: none;
    outline: none;
    cursor: pointer;
    border-radius: 5px;
  }
  .result {
    background: #ccc;
    border: 1px solid #f5f5f5;
    box-shadow: 0px 0px 5px 2px rgba(0, 0, 0, 0.05);
    border-radius: 10px;
  }
  .result .padding {
    padding: 20px;
  }
</style>
