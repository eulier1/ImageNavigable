<template>
  <div class="dropdown" @pointerdown="toggleMenu">
    <button
      class="bg-white hover:bg-gray-300 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
    >
      <div class="menu-icon">
        <div
          class="line1 bg-teal-700"
          :class="{'line1-forward': menuActive, 'line1-backward': !menuActive }"
        ></div>
        <div
          class="line2 bg-teal-700"
          :class="{'line2-forward': menuActive, 'line2-backward': !menuActive }"
        ></div>
        <div
          class="line3 bg-teal-700"
          :class="{'line3-forward': menuActive, 'line3-backward': !menuActive }"
        ></div>
      </div>
    </button>
    <!-- Dropdown Menu -->
    <div
      class="dropdown-menu"
      id="dropdown-menu"
      :class="{'block' : menuActive, 'hidden': !menuActive}"
      role="menu"
    >
      <div
        class="shadow pt-1 pb-1 bg-gray-100"
        :class="{'block' : menuActive, 'hidden': !menuActive}"
      >
        <img class="w-full" :src="urlLogo" alt="Placeholder" />
        <ul>
          <li
            class="block no-underline px-4 py-2 hover:bg-blue-500 hover:text-white font-lg text-base sm:text-lg md:text-xl lg:text-2xl xl:text-3xl"
            v-for="(map, i) in maps"
            :key="i+10"
            @pointerdown="switchMap(map.url, map.title, map.defaultZoom, map.zoomFactor)"
          >{{map.title}}</li>
        </ul>
      </div>
    </div>
    <!-- End Dropdown Menu -->
  </div>
</template>

<script>
export default {
  props: {
    maps: {
      type: Array,
      required: true
    },
    urlLogo: {
      type: String,
      default: "/placeholder.png"
    }
  },
  data() {
    return {
      menuActive: false
    };
  },
  methods: {
    switchMap(url, title, defaultZoom, zoomFactor) {
      this.mapTitle = title;
      this.$emit("updateMap", title, url, defaultZoom, zoomFactor);
    },
    toggleMenu() {
      this.menuActive = !this.menuActive;
    }
  }
};
</script>


<style>
.dropdown {
  position: relative;
  vertical-align: top;
}

.dropdown-menu {
  position: absolute;
  bottom: 100%;
  padding-bottom: 4px;
  padding-top: initial;
  top: auto;
}

.menu-icon {
  position: relative;
  width: 70px;
  height: 53px;
  cursor: pointer;
  z-index: 50;
  bottom: -2px;
  transform: scale(0.5);
  background: transparent;
  left: -2px;
}

.line1 {
  width: 100%;
  height: 8px;
}

.line2 {
  margin: 14px 0;
  width: 100%;
  height: 8px;
  opacity: 1;
}

.line3 {
  width: 100%;
  height: 8px;
}

/* Menu Icon Animations */

.line1-forward {
  transform: translate3d(0, 22px, 0) rotate(45deg);
  transition: all 0.3s;
}

.line2-forward {
  transform: scale(0);
  opacity: 0;
  transition: all 0.3s;
}

.line3-forward {
  transform: translate3d(0, -22px, 0) rotate(-45deg);
  transition: all 0.3s;
}

.line1-backward {
  transform: translate3d(0, 0, 0) rotate(0);
  transition: all 0.3s;
}

.line2-backward {
  opacity: 1;
  transition: all 0.3s;
}

.line3-backward {
  transform: translate3d(0, 0, 0) rotate(0);
  transition: all 0.3s;
}
</style>

