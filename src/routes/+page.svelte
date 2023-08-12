<script>
  import TinySegmenter from "tiny-segmenter";

  let wordList = [
    { word: "日本人", isWritten: false },
    { word: "昼ごはん", isWritten: false },
    { word: "食べる", isWritten: false },
    { word: "おすし", isWritten: false },
    { word: "ちがう", isWritten: false },
    { word: "てんぷら", isWritten: false },
    { word: "カレー", isWritten: false },
    { word: "読む", isWritten: false },
    { word: "雑誌", isWritten: false },
    { word: "すし", isWritten: false },
    { word: "じゃない", isWritten: false },
    { word: "食べ物", isWritten: false },
    { word: "わかる", isWritten: false },
    { word: "ちょっと", isWritten: false },
    { word: "からい", isWritten: false },
    { word: "行く", isWritten: false },
    { word: "いる", isWritten: false },
    { word: "いい", isWritten: false },
    { word: "日本", isWritten: false },
    { word: "ほんとうに", isWritten: false },
    { word: "そう", isWritten: false },
    { word: "たくさん", isWritten: false },
    { word: "思う", isWritten: false },
    { word: "大好き", isWritten: false },
    { word: "食べたい", isWritten: false },
    { word: "いつか", isWritten: false },
    { word: "来る", isWritten: false },
    { word: "も", isWritten: false },
    { word: "ほんとうに", isWritten: false },
    { word: "おいしい", isWritten: false },
  ];

  const segmenter = new TinySegmenter();
  let input = "";
  let segs = [""];

  $: segs = segmenter.segment(input);
  // $: commonWords = segs.filter((word) => wordList.includes(word));
  function updateIsWritten() {
    wordList = wordList.map((obj) => ({
      ...obj,
      isWritten: segs.includes(obj.word),
    }));
  }
</script>

<div class="app">
  <div class="word_list">
    {#each wordList as word}
      {#if word.isWritten}
        <div class={"word word_true"}>{word.word}</div>
      {:else}
        <div class={"word"}>{word.word}</div>
      {/if}
    {/each}
  </div>
  <textarea class="input" bind:value={input} on:input={updateIsWritten} />
</div>
<button on:click={updateIsWritten}>Update</button>

<!-- <p>Used words: {commonWords.length}</p>
{#each commonWords as word}
  <p>{word}</p>
{/each} -->

<style>
  .app {
    display: flex;
  }
  .word {
    padding: 1rem;
    border: 1px solid #384856;
    border-radius: 0.2rem;
  }
  .word_true {
    border: 1px solid #3b8b50;
    background-color: #152715;
  }
  .input {
    resize: none;
  }
</style>
