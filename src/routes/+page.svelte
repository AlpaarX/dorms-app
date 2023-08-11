<script>
  let input = "";
  let resultText = "";
    function segmentText() {
    const rmaJa = new RakutenMA(model_ja);
    rmaJa.featset = RakutenMA.default_featset_ja;
    rmaJa.hash_func = RakutenMA.create_hash_func(15);

    const text = input;

    const convertedText = HanZenKaku.hs2fs(
      HanZenKaku.hw2fw(HanZenKaku.h2z(text))
    );
    const tokens = rmaJa.tokenize(convertedText);

    resultText = tokens ? RakutenMA.tokens2string(tokens) : "";
  }
</script>

<svelte:head>
  <script
    type="text/javascript"
    src="node_modules/rakutenma/rakutenma.js"
    charset="UTF-8"
  ></script>
  <script
    type="text/javascript"
    src="node_modules/rakutenma/model_ja.js"
    charset="UTF-8"
  ></script>
  <script
    type="text/javascript"
    src="node_modules/rakutenma/hanzenkaku.js"
    charset="UTF-8"
  ></script>
</svelte:head>
<main>
  <div class="container">
    <p id="output">{resultText}</p>
    <button on:click={segmentText}></button>
  </div>
</main>
