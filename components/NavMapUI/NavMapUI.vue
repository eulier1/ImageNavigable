<template>
  <section class="nav-wrapper">
    <div class="flex flex-row justify-center">
      <up-arrow class="flex flex-col" @pointerdown="$emit('move-up', $event.target)"></up-arrow>
    </div>

    <div class="flex flex-row justify-center">
      <left-arrow class="flex-col" @pointerdown="$emit('move-left', $event.target)"></left-arrow>
      <reset class="flex-row p-1" @pointerdown="$emit('reset', $event.target)"></reset>
      <right-arrow class="flex-col" @pointerdown="$emit('move-right', $event.target)"></right-arrow>
    </div>
    <div class="flex flex-row justify-center">
      <down-arrow class="flex-col" @pointerdown="$emit('move-down', $event.target)"></down-arrow>
    </div>
  </section>
</template>

<script>
import UpArrow from "./UpArrow";
import DownArrow from "./DownArrow";
import LeftArrow from "./LeftArrow";
import RightArrow from "./RightArrow";
import Reset from "./Reset";

export default {
  components: {
    UpArrow,
    DownArrow,
    LeftArrow,
    RightArrow,
    Reset
  }
};
</script>

<style scoped>
.nav-wrapper {
  position: absolute;
  width: 100%;
  height: auto;
}
</style>

