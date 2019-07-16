<template>
  <section class="view-wrapper">
    <div ref="viewContainer" class="view-container">
      <img
        class="center"
        ref="imageRendered"
        :src="urlImage"
        :style="{transform: `scale(${zoom}) translate(${translateX + '%'}, ${translateY + '%'})`}"
        alt="Map"
      />
      <nav class="ui-zoom">
        <ul>
          <li>
            <button
              @click="zoomIn"
              class="bg-white hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
            >
              <img width="25" src="zoomIn.png" class="opacity-75" alt="zoom in" />
            </button>
          </li>
          <li>
            <button
              @click="zoomReset"
              class="bg-white hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
            >
              <img width="25" src="reset.png" class="opacity-75" alt="reset zoom" />
            </button>
          </li>
          <li>
            <button
              @click="zoomOut"
              class="bg-white hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
            >
              <img width="25" src="zoomOut.png" class="opacity-75" alt="zoom out" />
            </button>
          </li>
        </ul>
      </nav>
      <nav class="ui-swith-map">
        <button
          @click="urlImage = 'maps/Miami.png'"
          class="bg-white hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
        >Map 1</button>
        <button
          @click="urlImage = 'maps/Washingtong.png'"
          class="bg-white hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
        >Map 2</button>
        <button
          @click="urlImage = 'maps/Portland.png'"
          class="bg-white hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
        >Map 3</button>
      </nav>
      <nav
        class="ui-navigation"
        :style="{ background: `url('navigation.png')`, backgroundPosition: `0px ${spriteHeight}px` }"
      >
        <div
          class="up-arrow"
          @click="moveUp"
          @mouseover="spriteHeight = -44"
          @mouseleave=" spriteHeight = 0"
        ></div>
        <div
          class="left-arrow"
          @click="moveLeft"
          @mouseover="spriteHeight = -176"
          @mouseleave=" spriteHeight = 0"
        ></div>
        <div
          class="right-arrow"
          @click="moveRight"
          @mouseover="spriteHeight = -88"
          @mouseleave=" spriteHeight = 0"
        ></div>
        <div
          class="down-arrow"
          @click="moveDown"
          @mouseover="spriteHeight = -132"
          @mouseleave=" spriteHeight = 0"
        ></div>
      </nav>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      zoom: 1,
      translateX: 0,
      translateY: 0,
      spriteHeight: 0,
      urlImage: "maps/Miami.png"
    };
  },
  methods: {
    zoomReset() {
      this.zoom = 1;
      this.translateX = 0;
      this.translateY = 0;
    },
    zoomIn() {
      this.zoom < 4 ? (this.zoom += 0.5) : null;
    },
    zoomOut() {
      this.zoom > 1 ? (this.zoom -= 0.5) : null;
    },
    moveUp() {
      const viewContainerBox = this.$refs.viewContainer.getBoundingClientRect();
      const imageRenderedBox = this.$refs.imageRendered.getBoundingClientRect();
      if (this.zoom > 1 && imageRenderedBox.top < viewContainerBox.top) {
        this.translateY += 5;
      }
    },
    moveDown() {
      const viewContainerBox = this.$refs.viewContainer.getBoundingClientRect();
      const imageRenderedBox = this.$refs.imageRendered.getBoundingClientRect();
      if (this.zoom > 1 && imageRenderedBox.bottom > viewContainerBox.bottom) {
        this.translateY -= 5;
      }
    },
    moveLeft() {
      const viewContainerBox = this.$refs.viewContainer.getBoundingClientRect();
      const imageRenderedBox = this.$refs.imageRendered.getBoundingClientRect();
      if (this.zoom > 1 && imageRenderedBox.left < viewContainerBox.left) {
        this.translateX += 5;
      }
    },
    moveRight() {
      const viewContainerBox = this.$refs.viewContainer.getBoundingClientRect();
      const imageRenderedBox = this.$refs.imageRendered.getBoundingClientRect();
      if (this.zoom > 1 && imageRenderedBox.right > viewContainerBox.right) {
        this.translateX -= 5;
      }
    }
  }
};
</script>

<style scoped>
.view-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
}

.view-container {
  position: absolute;
  background: #333;
  z-index: 1;
  width: 100%;
  padding: 1rem;
  overflow: hidden;
}

.ui-zoom {
  position: absolute;
  top: 1rem;
  right: 1rem;
}

.ui-swith-map {
  position: absolute;
  bottom: 1rem;
  left: 1rem;
}

.ui-navigation {
  width: 45px;
  height: 44px;
  position: absolute;
  top: 2rem;
  left: 2rem;
  transform: scale(1.5);
}

.up-arrow {
  position: absolute;
  width: 15px;
  height: 15px;
  left: 15px;
}

.left-arrow {
  position: absolute;
  width: 15px;
  height: 15px;
  top: 12px;
  left: 1px;
}

.right-arrow {
  position: absolute;
  width: 15px;
  height: 15px;
  right: 1px;
  top: 12px;
}

.down-arrow {
  position: absolute;
  width: 15px;
  height: 15px;
  bottom: 0;
  left: 15px;
}

.center {
  margin: auto;
}
</style>

