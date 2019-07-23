<template>
  <section class="nav-wrapper">
    <div class="flex flex-row justify-center">
      <up-arrow
        class="flex flex-col"
        @mouseenter="$emit('mouseenter',$event.target)"
        @mouseleave="$emit('mouseleave',$event.target)"
        @pointerdown="$emit('move-up', $event.target)"
      ></up-arrow>
    </div>

    <div class="flex flex-row justify-center">
      <left-arrow
        class="flex-col"
        @mouseenter="$emit('mouseenter',$event.target)"
        @mouseleave="$emit('mouseleave',$event.target)"
        @pointerdown="$emit('move-left', $event.target)"
      ></left-arrow>
      <reset
        class="flex-row p-1"
        @mouseenter="$emit('mouseenter',$event.target)"
        @mouseleave="$emit('mouseleave',$event.target)"
        @pointerdown="$emit('reset', $event.target)"
      ></reset>
      <right-arrow
        class="flex-col"
        @mouseenter="$emit('mouseenter',$event.target)"
        @mouseleave="$emit('mouseleave',$event.target)"
        @pointerdown="$emit('move-right', $event.target)"
      ></right-arrow>
    </div>
    <div class="flex flex-row justify-center">
      <down-arrow
        class="flex-col"
        @mouseenter="$emit('mouseenter',$event.target)"
        @mouseleave="$emit('mouseleave',$event.target)"
        @pointerdown="$emit('move-down', $event.target)"
      ></down-arrow>
    </div>
  </section>
</template>

<script>
import UpArrow from "./Controls/UpArrow";
import DownArrow from "./Controls/DownArrow";
import LeftArrow from "./Controls/LeftArrow";
import RightArrow from "./Controls/RightArrow";
import Reset from "./Controls/Reset";

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

