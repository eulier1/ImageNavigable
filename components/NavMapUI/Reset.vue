<template>
  <svg
    @pointerdown="pointerDown"
    @pointerup="pointerUp"
    version="1.1"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    x="0px"
    y="0px"
    viewBox="0 0 60 60"
    style="enable-background:new 0 0 60 60;"
    xml:space="preserve"
    :width="width"
  >
    <path
      :style="{'fill':fillColor}"
      d="M30,0C13.458,0,0,13.458,0,30s13.458,30,30,30s30-13.458,30-30S46.542,0,30,0z M30,58C14.561,58,2,45.439,2,30
	S14.561,2,30,2s28,12.561,28,28S45.439,58,30,58z"
    />
    <!-- <div>
      Icons made by
      <a
        href="https://www.flaticon.com/authors/smashicons"
        title="Smashicons"
      >Smashicons</a> from
      <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by
      <a
        href="http://creativecommons.org/licenses/by/3.0/"
        title="Creative Commons BY 3.0"
        target="_blank"
      >CC 3.0 BY</a>
    </div>-->
  </svg>
</template>

<script>
export default {
  props: {
    width: {
      type: Number,
      default: 25
    }
  },
  data() {
    return {
      fillColor: "#222"
    };
  },
  methods: {
    pointerDown(ev) {
      this.fillColor = "lightblue";
      this.$emit("pointerdown", ev);
    },
    pointerUp() {
      this.fillColor = "#222";
    }
  }
};
</script>
