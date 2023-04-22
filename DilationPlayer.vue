<template>
  <div id="video">
    <div class="dp">
      <div class="dp-logo"></div>
      <video class="dp-player" controlslist="nodownload" autoplay="true"></video>
      <div class="dp-overlay">
        <div class="dp-overlay-loader active">
          <div class="dp-overlay-icon dp-overlay-loader-icon"></div>
        </div>
        <div class="dp-overlay-player active">
          <div class="dp-overlay-icon dp-overlay-player-icon"></div>
        </div>
      </div>
      <!-- <div class="dp-overlay-error dp-overlay">
        <div class="dp-overlay-icon">ERROR</div>
      </div> -->
      <div class="dp-menu">
        <div class="dp-menu-list"></div>
      </div>
      <div class="dp-ads">
        <div class="dp-ads-item">
          <button class="dp-ads-close"></button>
          <div class="dp-ads-content"></div>
        </div>
      </div>
      <div class="dp-subtitles"></div>
      <div class="dp-panel active">
        <div class="dp-progress">
          <div class="dp-progress-overlay"></div>
          <div class="dp-progress-tooltip-image"></div>
          <span class="dp-progress-tooltip-text"></span>
          <div class="dp-progress-line">
            <div class="dp-progress-line-bg"></div>
            <div class="dp-progress-line-loading"></div>
            <div class="dp-progress-tooltip-line"></div>
            <div class="dp-progress-line-playing"></div>
          </div>
        </div>
        <div class="dp-control">
          <div>
            <button class="dp-btn-play left"></button>
            <div class="dp-group left">
              <button class="dp-btn-volume"></button>
              <div class="dp-volume-tooltip">
                <input class="dp-volume-range" type="range" min="0" max="1" step="0.01">
              </div>
            </div>
            <button class="dp-timer"></button>
            <button class="right dp-btn-fullscreen"></button>
            <button class="right dp-btn-actualscreen"></button>
            <!-- <button class="right dp-btn-subtitle"></button> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DilationPlayer from '@dilation-player/core';
import Ext from '@dilation-player/extensions';
import AdsExtension from '@dilation-player/ads';
import messages from './locales';
export default {
  props: ['data'],

  data() {
    return {
      video: null
    }
  },

  mounted() {
    this.video = new DilationPlayer('#video', {
      extensions: [
        Ext.Config,
        Ext.Event,
        Ext.Translator,
        Ext.Menu,
        Ext.Logo,
        Ext.Overlay,
        Ext.Panel,
        Ext.Control,
        Ext.Play,
        Ext.Progress,
        Ext.Preview,
        Ext.Sound,
        Ext.Screen,
        Ext.Source,
        Ext.Subtitle,
        Ext.View,
        AdsExtension
      ],
      messages,
      ...this.data
    });

    // Event
    this.video.$event.listen('*', (e) => {
      this.$emit('listen', e);
    });
  }
}
</script>
