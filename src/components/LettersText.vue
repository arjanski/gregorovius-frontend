<template>
  <v-runtime-template :template="data"></v-runtime-template>
</template>

<script>
import VRuntimeTemplate from "v-runtime-template";
import { xslt } from "@/mixins/xslt";
import { dataService } from "@/shared";

export default {
  name: "LettersText",
  components: {
    VRuntimeTemplate
  },
  mixins: [xslt],
  data() {
    return {
      data: null
    };
  },

  mounted() {
    this.getItems();
  },

  methods: {
    async getItems() {
      try {
        const response = await dataService.XSLTransform(this.$route.path, "LettersText");
        const data = await response;
        this.data = data;
      } catch (error) {
        // eslint-disable-next-line
        console.error(error)
      }
    }
  }
};
</script>

<style>
.g-edition-text {
  font-family: Cardo;
  font-size: 14pt;
  padding: 16px;
}

span.g-pb {
  display: block;
  position: absolute;
  left: 1em;
  margin-top: -1.7em;
  font-size: 0.8em;
}

span.g-add {
  color: green;
}

del {
  color: red;
}

.g-entity-link {
  box-shadow: inset 0 -0.7rem 0 0 hsla(144.9, 100%, 82.5%, 0.5);
  transition: box-shadow 0.5s;
  cursor: pointer;
}
.g-entity-link.start-offset {
  box-shadow: inset 0 -2.5rem 0 0 hsla(144.9, 100%, 82.5%, 1);
}
.g-entity-link.start-offset:hover {
  box-shadow: inset 0 -0.5rem 0 0 hsla(144.9, 100%, 82.5%, 1);
}

.g-entity-link:hover {
  box-shadow: inset 0 -2.5rem 0 0 hsla(144.9, 100%, 82.5%, 1);
}

.g-mprint {
  font-family: "Courier New", Courier, monospace;
  font-size: 12pt;
  letter-spacing: 2px;
}

.g-aq {
  font-family: "IBMPlexSans";
  font-size: 13pt;
}

.g-margin-right {
  display: block;
  position: absolute !important;
  right: 0em;
}

.g-coupled {
  display: inline;
}

span.g-list {
  display: block;
  margin-bottom: 1em;
}

span.g-list-item {
  display: flex;
  margin-bottom: 0.5em;
  margin-left: 1.5rem;
}
</style>
