<script>
  export let sharetext = "",
    sharetitle = "",
    shareurl = location.href,
    shareimg = undefined;

  let share;

  if (shareimg && navigator.canShare) {
    share = async function() {
      const response = await fetch(shareimg);
      const blob = await response.blob();
      const files = await new File([blob], "image.jpeg");
      console.log(files);

      navigator.share({
        url: shareurl,
        title: sharetitle,
        text: sharetext,
        files: [files]
      });
    };
  } else {
    share = function() {
      navigator.share({
        url: shareurl,
        title: sharetitle,
        text: sharetext
      });
    };
  }
</script>

{#if window.navigator.share}
  <button on:click={share}>Share</button>
{/if}
