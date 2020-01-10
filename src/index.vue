<template>
  <div>
    <input class="" type="text" v-model="input" @keypress.enter="depackURL" />
    {{ this.data }}
    {{ this.input }}
    {{ this.items }}
    <div class="tags-container">
      <tag
        v-for="(tag, idx) in tags"
        :key="`tag-${idx}`"
        :label="tag[0]"
        :value="tag[1]"
      />
    </div>
  </div>
</template>

<script>
import { rules } from "../config.json";
import Tag from "./Tag";

export default {
  components: {
    Tag
  },

  data() {
    return {
      input: null,
      currentLabel: null,
      currentLabelIndex: 0,
      labels: [],
      data: {},
      tags: null,
      items: null
    };
  },

  methods: {
    //     inputDone() {
    //       if (!this.data.provider) {
    //         this.depackURL();
    //       }
    //       this.toNextLabel();
    //     },
    depackURL() {
      const [provider, ...items] = this.input.match(
        /(\b(?!http|www|com|watch))([\w-]+)/gm
      );

      const attributes = items.reduce((acc, item) => {
        rules[provider].forEach(rule => {
          if (Object.values(rule).indexOf(item) > -1) {
            rule.items.map((ruleItem, i) => {
              acc[ruleItem] = items[i];
            });
          }
        });
        return acc;
      }, {});

      this.data = {
        provider,
        ...attributes
      };
      this.items = items;

      this.clearInput();
      this.populateTags();
    },

    clearInput() {
      this.input = "";
    },

    populateTags() {
      this.tags = Object.entries(this.data);
    }
    //     addLabel(label, value) {
    //       this.data[label] = value;
    //     },
    //     removeLabel(label) {
    //       if (label in this.data) {
    //         delete this.data[label];
    //       }
    //     },
    //     writeNewLabel(input) {
    //       const pairs = input.split(",");
    //       pairs.forEach(([label, value]) => this.addLabel(label, value));
    //     },
    //     checkIfValidLabel(label) {},
    //     toNextLabel() {},
    //     clearLabel() {
    //       this.currentLabel = "";
    //     }
  }
};
</script>

<style>
.tags-container {
  margin: 10px;
  display: flex;
}
</style>
