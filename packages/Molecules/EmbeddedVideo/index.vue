<template>
  <div class="rpl-embedded-video">
    <div class="rpl-embedded-video-iframe-container">
      <iframe class="rpl-embedded-video-frame" :width="width" :height="height" :src="src" :lang="lang" allowfullscreen></iframe>
    </div>
    <div v-if="variant === 'link'" class="rpl-embed-video__link" >
      <rpl-icon symbol="view" color="primary" />
      <rpl-text-link :url="url" :text="mediaLink" />
    </div>
    <div v-if="variant === 'full'" class="rpl-embed-video__transcript" >{{ transcript }}</div>
  </div>
</template>

<script>
import { RplTextLink } from '@dpc-sdp/ripple-link'
import RplIcon from '@dpc-sdp/ripple-icon'

export default {
  name: 'RplEmbeddedVideo',
  props: {
    width: String,
    height: String,
    src: String,
    lang: String,
    variant: String,
    url: String,
    transcript: String,
    mediaLink: String
  },
  components: {
    RplTextLink,
    RplIcon
  }
}
</script>

<style lang="scss">
  @import "~@dpc-sdp/ripple-global/style";

  $rpl-embedded-video-padding-bottom: 56.25% !default;
  $rpl-embedded-video-padding-top: $rpl-space-4;
  $rpl-embedded-video-transcript-padding: $rpl-space-4 0 $rpl-space-4;
  $rpl-embedded-video-height: 0;

  .rpl-embedded-video-iframe-container {
    position: relative;
    padding-bottom: $rpl-embedded-video-padding-bottom;
    padding-top:$rpl-embedded-video-padding-top;
    height: $rpl-embedded-video-height;
    overflow: hidden;
  }

  iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }

  .rpl-embed-video__transcript {
    padding: $rpl-embedded-video-transcript-padding;
  }
</style>
