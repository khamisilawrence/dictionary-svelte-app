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
  {/if}
  {#each wordData.meanings as meaning}
    <div class="meaning">
      <!--  -->
      <div class="part-of-speech">
        &bull; {meaning.partOfSpeech}
      </div>
      <div class="definitions">
        {#each meaning.definitions as definition}
          <div class="definition">
            <p>
              Definition: <b>{definition.definition}</b>
            </p>
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
  }
  .word-data .audios .audio {
    padding: 8px 20px;
  }
  .word-data .meaning {
    padding: 8px 20px;
    border-bottom: 1px solid #ddd;
  }
  .word-data > div:last-child {
    border-bottom: none;
  }
  .word-data .meaning .definitions .definition {
    padding: 8px 0px;
  }
  .word-data .meaning .definitions .definition {
    margin: 5px 0px;
  }
</style>
