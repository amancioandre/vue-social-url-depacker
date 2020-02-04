<template>
  <div class="tag">
    <div class="label-header">
      <small class="label">{{ label }}</small>
    </div>
    <div class="value">{{ value }}</div>
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
  height: 40px;
  padding: 5px 10px;
  margin: 5px;
  border: none;
  border-radius: 20px;
  background-color: #f0f4f7;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.label-header {
  display: flex;
  justify-content: flex-start;
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
  margin-left: auto;
  font-size: 12px;
  font-family: Helvitica;
}
</style>
