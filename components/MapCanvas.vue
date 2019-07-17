<template>
  <section class="view-wrapper">
    <div ref="viewContainer" class="view-container">
      <div ref="imageContainer" class="imageContainer" v-dragged.prevent="onDragged">
        <img
          ref="imageRendered"
          :src="urlImage"
          :style="{'transform': `scale(${zoom}) translate(${translateX + '%'}, ${translateY + '%'})`, 'weigth': '100%', 'height' : '100%' , 'margin': 'auto'}"
          alt="Map"
        />
      </div>
      <nav class="ui-zoom">
        <ul class="flex">
          <li>
            <button
              @pointerdown="zoomIn"
              class="bg-white hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
            >
              <img width="25" src="zoomIn.png" class="opacity-75" alt="zoom in" />
            </button>
          </li>
          <!-- <li>
            <button
              @pointerdown="reset"
              class="bg-white hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
            >
              <img width="25" src="reset.png" class="opacity-75" alt="reset zoom" />
            </button>
          </li>-->
          <li>
            <button
              @pointerdown="zoomOut"
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
            <li
              class="block no-underline px-4 py-2 hover:bg-blue-500 hover:text-white"
              v-for="(map, i) in maps"
              :key="i+10"
              @pointerdown="switchMap(map.url, map.title)"
            >{{map.title}}</li>
          </ul>
        </t-dropdown>
      </nav>
      <nav class="ui-navigation">
        <nav-map-ui
          @move-up="moveUp"
          @move-down="moveDown"
          @move-right="moveRight"
          @move-left="moveLeft"
          @reset="reset"
        ></nav-map-ui>
      </nav>
    </div>
  </section>
</template>

<script>
import NavMapUi from "./NavMapUI/NavMapUI";

export default {
  components: {
    NavMapUi
  },
  data() {
    return {
      mapTitle: "",
      maps: [
        {
          url: "maps/portrait.jpg",
          title: "Portrait"
        },
        {
          url: "maps/landscape.jpg",
          title: "Landscape"
        },
        {
          url: "maps/square.jpg",
          title: "Square"
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
  mounted() {
    console.log();
  },
  methods: {
    initMap() {
      this.mapTitle = this.maps[0].title;
      this.urlImage = this.maps[0].url;
    },
    reset() {
      this.zoom = 1;
      this.translateX = 0;
      this.translateY = 0;
      this.$refs.imageContainer.style.top = "0";
      this.$refs.imageContainer.style.left = "0";
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
  width: 100vw;
  height: 100vh;
}

.view-container {
  position: absolute;
  background: #555;
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
  width: 75px;
  height: 75px;
  position: absolute;
  bottom: 5.5rem;
  right: 2.5rem;
  transform: scale(1.5);
}

.imageContainer {
  position: relative;
  width: 100%;
  height: 100%;
}
</style>

