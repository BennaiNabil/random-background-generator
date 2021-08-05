<template>

  <div id="app">

    <md-toolbar class="md-accent" md-elevation="3">
      <h3 class="md-title" style="flex: 1">Random Background Generator</h3>
      <md-button>About Me</md-button>
      <md-button class="md-primary">Source code</md-button>
    </md-toolbar>

    <div class="p-5">
      <md-card class="text-center my-5 mx-auto p-5" md-with-hover v-bind:style="this.cardStyle">
        <md-card-header>
          <div class="md-title">
            Bored of this card's colour? Click below to change its background !
          </div>
        </md-card-header>

        <md-card-actions>
          <md-button v-bind:style="this.cardStyle" @click="generateHexColor()">
            Change Me!
          </md-button>
        </md-card-actions>
      </md-card>
    </div>

    <div class="p-5">
      <md-card class="text-center py-5" md-with-hover>
        <md-card-header>
          <div class="md-title">
            {{ cardStyle.backgroundColor }}
          </div>
        </md-card-header>
      </md-card>
    </div>

  </div>

</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      cardStyle: {backgroundColor: "#fff", color: "#000"},
    };
  },
  methods: {
    /**
     * Generates a new cardStyle object {backgroundcolor: XXX, color: YYY}
     * XXX : The card's background color in Hexadecimal format
     * YYY : The text's color ("white"/'black') whether XXX is computed to be bright or not in isColorLight()
     */
    generateHexColor: function () {
      let bgColor = Math.floor(Math.random() * 16777215).toString(16);
      let textColor = this.isColorLight(`#${bgColor}`) ? "black" : "white";
      this.cardStyle = {backgroundColor: `#${bgColor}`, color: `${textColor}`};
    },
    /**
     * Returns whether or not the color entered as an argument is perceived as
     * bright to the human eye.
     * Used to avoid contrast problems in the card's display
     * @param color
     * @returns {boolean}
     */
    isColorLight: function (color) {
      const hexadecimalValue = color.replace("#", "");
      const redComponent = parseInt(hexadecimalValue.substr(0, 2), 16);
      const greenComponent = parseInt(hexadecimalValue.substr(2, 2), 16);
      const blueComponent = parseInt(hexadecimalValue.substr(4, 2), 16);
      const computedBrightness = (redComponent * 299 + greenComponent * 587 + blueComponent * 114) / 1000;
      return computedBrightness > 155;
    },
  },
};
</script>

<style></style>
