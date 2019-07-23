<template>
  <svg
    @pointerdown="pointerDown"
    @pointerup="pointerUp"
    @mouseenter="$emit('mouseenter',$event.target)"
    @mouseleave="$emit('mouseleave',$event.target)"
    xmlns:dc="http://purl.org/dc/elements/1.1/"
    xmlns:cc="http://creativecommons.org/ns#"
    xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
    xmlns:svg="http://www.w3.org/2000/svg"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:sodipodi="http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd"
    xmlns:inkscape="http://www.inkscape.org/namespaces/inkscape"
    version="1.1"
    x="0px"
    y="0px"
    viewBox="0 0 254.296 254.296"
    style="enable-background:new 0 0 254.296 254.296;"
    xml:space="preserve"
    sodipodi:docname="left.svg"
    inkscape:version="0.92.3 (2405546, 2018-03-11)"
    :width="width"
  >
    <metadata id="metadata45">
      <rdf:RDF>
        <cc:Work rdf:about>
          <dc:format>image/svg+xml</dc:format>
          <dc:type rdf:resource="http://purl.org/dc/dcmitype/StillImage" />
          <dc:title />
        </cc:Work>
      </rdf:RDF>
    </metadata>
    <defs id="defs43" />
    <sodipodi:namedview
      pagecolor="#ffffff"
      borderColor="#666666"
      borderopacity="1"
      objecttolerance="10"
      gridtolerance="10"
      guidetolerance="10"
      inkscape:pageopacity="0"
      inkscape:pageshadow="2"
      inkscape:window-width="1360"
      inkscape:window-height="705"
      id="namedview41"
      showgrid="false"
      inkscape:zoom="0.92805233"
      inkscape:cx="127.148"
      inkscape:cy="127.148"
      inkscape:window-x="0"
      inkscape:window-y="30"
      inkscape:window-maximized="1"
      inkscape:current-layer="Capa_1"
    />
    <g id="g8" transform="rotate(-90,127.14762,127.14762)">
      <g id="g6">
        <g id="g4">
          <path
            :style="{'fill':fillColor}"
            d="M 249.628,176.101 138.421,52.88 c -6.198,-6.929 -16.241,-6.929 -22.407,0 L 115.633,53.516 4.648,176.101 c -6.198,6.897 -6.198,18.052 0,24.981 l 0.191,0.159 c 2.892,3.305 6.865,5.371 11.346,5.371 h 221.937 c 4.577,0 8.613,-2.161 11.41,-5.594 l 0.064,0.064 c 6.261,-6.929 6.261,-18.084 0.032,-24.981 z"
            id="path2"
            inkscape:connector-curvature="0"
          />
        </g>
      </g>
    </g>
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
