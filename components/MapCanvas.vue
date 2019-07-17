<template>
  <section class="view-wrapper">
    <div ref="viewContainer" class="view-container">
      <div style="position: relative" v-dragged.prevent="onDragged">
        <img
          class="map"
          ref="imageRendered"
          :src="urlImage"
          :style="{'transform': `scale(${zoom}) translate(${translateX + '%'}, ${translateY + '%'})` }"
          alt="Map"
        />
      </div>
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
        <t-dropdown :text="mapTitle" placement="top">
          <ul>
            <li v-for="(map, i) in maps" :key="i+10">
              <a
                href="#"
                @click="switchMap(map.url, map.title)"
                class="block no-underline px-4 py-2 hover:bg-blue-500 hover:text-white"
              >{{map.title}}</a>
            </li>
          </ul>
        </t-dropdown>
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
      mapTitle: "",
      maps: [
        {
          url: "maps/Miami.png",
          title: "Miami"
        },
        {
          url: "maps/Washingtong.png",
          title: "Washington"
        },
        {
          url: "maps/Portland.png",
          title: "Portland"
        }
      ],
      zoom: 1,
      translateX: 0,
      translateY: 0,
      spriteHeight: 0,
      urlImage: "maps/Miami.png"
    };
  },
  created() {
    this.initMap();
  },
  methods: {
    initMap() {
      this.mapTitle = this.maps[0].title;
      this.urlImage = this.maps[0].url;
    },
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
    },
    switchMap(url, title) {
      this.mapTitle = title;
      this.urlImage = url;
    },
    onDragged({
      el,
      deltaX,
      deltaY,
      offsetX,
      offsetY,
      clientX,
      clientY,
      first,
      last
    }) {
      if (first) {
        this.isDragging = true;
        return;
      }
      if (last) {
        this.isDragging = false;
        return;
      }
      var l = +window.getComputedStyle(el)["left"].slice(0, -2) || 0;
      var t = +window.getComputedStyle(el)["top"].slice(0, -2) || 0;
      el.style.left = l + deltaX + "px";
      el.style.top = t + deltaY + "px";
    }
  }
};
</script>

<style scoped>
.view-wrapper {
  position: relative;
  width: 100vw;
  height: 100vh;
}

.view-container {
  position: absolute;
  background: #333;
  z-index: 1;
  width: 100%;
  height: 100%;
  padding: 1rem;
  overflow: hidden;
}

.ui-zoom {
  position: absolute;
  bottom: 1rem;
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
  bottom: 2rem;
  right: 6rem;
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

.map {
  margin: auto;
  height: 100%;
}
</style>

