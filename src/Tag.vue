<template>
  <div class="tag">
    <span class="label">
      <small>{{ label }}</small>
    </span>
    <div class="value">
      {{ value }}
    </div>
    <div class="close">
      x
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    value: {
      type: String,
      required: true
    }
  },

  methods: {
    remove() {
      this.$emit("removed", this.label);
    }
  }
};
</script>

<style>
.tag {
  position: relative;
  height: 40px;
  padding: 5px 10px;
  margin: 5px;
  border: none;
  border-radius: 20px;
  background-color: #f0f4f7;
  display: flex;
  flex-direction: column;
}

.label {
  font-family: Helvetica;
  font-size: 12px;
  color: black;
}

.value {
  padding: 5px 0px;
  font-family: Helvetica;
  font-size: 16px;
  color: #685cf5;
}

.close {
  position: absolute;
  top: 2px;
  right: 12px;
  font-size: 12px;
  font-family: Helvitica;
}
</style>
