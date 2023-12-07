<script>
  export let wordData = null;
  function playAudio(src) {
    let audio = new Audio(src);
    audio.play();
  }
</script>

<div class="word-data">
  {#if wordData.phonetics}
    <div class="audios">
      <span>
        <p>Pronounciation:</p>
      </span>
      <div class="group">
        {#each wordData.phonetics as data}
          <div class="audio">
            <p>
              {data.text}
              <i
                class="fa fa-play-circle"
                on:click={() => playAudio(data.audio)}
                on:keyup
              ></i>
            </p>
          </div>
        {/each}
      </div>
    </div>
  {/if}
  {#each wordData.meanings as meaning}
    <div class="meaning">
      <!--  -->
      <div class="part-of-speech">
        &bull; {meaning.partOfSpeech}
      </div>
      <div class="definitions">
        <span>Definitions:</span>
        {#each meaning.definitions as definition}
          <div class="definition">
            <ul>
              <li>{definition.definition}</li>
            </ul>
            {#if definition.example}
              <p>
                Example: <i>
                  {definition.example}
                </i>
              </p>
            {/if}
          </div>
        {/each}
      </div>
    </div>
  {/each}
</div>

<style>
  .word-data .audios {
    border-bottom: 1px solid #ddd;
    display: block;
    padding-top: 4px;
    padding-left: 20px;
    padding-bottom: 4px;
    @media screen and (min-width: 640px) {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      padding-left: 0;
      padding-bottom: 0;
    }
  }
  .word-data .audios span {
    padding-left: 20px;
  }
  .word-data .audios span p {
    font-weight: bold;
  }
  .word-data .audios .group {
    display: flex;
  }
  .word-data .audios .audio {
    padding: 8px 20px;
  }
  .word-data .audios .audio p i {
    cursor: pointer;
  }
  .word-data .meaning {
    padding: 8px 20px;
    border-bottom: 1px solid #ddd;
  }
  .word-data > div:last-child {
    border-bottom: none;
  }
  .word-data .part-of-speech {
    background: #eee;
    width: fit-content;
    padding: 2px 4px;
    border-radius: 6px;
    text-transform: capitalize;
    margin: 10px 0;
  }
  .word-data .meaning .definitions span {
    font-weight: bold;
  }
  .word-data .meaning .definitions .definition {
    padding: 8px 0px;
    margin: 5px 0px;
  }
  .word-data .meaning .definitions .definition ul {
    padding: 0 20px;
  }
</style>
