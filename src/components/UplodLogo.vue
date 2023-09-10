<template>
  <div class="container py-5">
    <div class="text-center py-4">
      <span
        class="ms-2"
        style="
          display: inline-block;
          width: 30px;
          height: 30px;
          background-color: #c0dd49;
          color: white;
          text-align: center;
          border-radius: 50%;
          font-weight: bold;
        "
        >2</span
      >قم بتحميل الشعار الخاص بك بصيغة PNG
      <div>
        <div class="file-input py-5">
          <input
            type="file"
            name="file-input"
            id="file-input"
            class="file-input__input"
          />
          <label class="file-input__label" for="file-input">
            <i class="fa-solid fa-cloud-arrow-up icon-size"></i>
          </label>
        </div>
      </div>
    </div>

    <div class="text-center">
      <span
        class="ms-2"
        style="
          display: inline-block;
          width: 30px;
          height: 30px;
          background-color: #c0dd49;
          color: white;
          text-align: center;
          border-radius: 50%;
          font-weight: bold;
        "
        >3</span
      >قم بكتابة عبارة التهنئة
      <div class="py-4">
        <textarea
          v-model="inputText"
          @input="updateCharacterCount"
          class="custom-textarea"
          :class="{ exceeded: isExceeded }"
        ></textarea>
        <div :class="{ 'character-count': true, exceeded: isExceeded }">
          {{ characterCount }} / {{ maxChars }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.file-input__input {
  width: 0.1px;
  height: 0.1px;
  opacity: 0;
  overflow: hidden;
  position: absolute;
  z-index: -1;
}

.file-input__label {
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  border-radius: 10px;
  font-size: 14px;
  font-weight: 600;
  color: #fff;
  font-size: 14px;
  padding: 15px 43px;
  background-color: #4a7c95;
  box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.25);
}

.file-input__label svg {
  height: 16px;
  margin-right: 4px;
}
.icon-size {
  font-size: 25px;
}
.custom-textarea {
    width: 40%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 10px;
    font-size: 16px;
    resize: vertical;
    height: 50px;
}

.character-count {
  margin-top: 8px;
  color: black;
}

.exceeded {
  color: red;
}
</style>
<script>
export default {
  data() {
    return {
      inputText: "",
      maxChars: 24,
    };
  },
  computed: {
    characterCount() {
      return this.inputText.length;
    },
    isExceeded() {
      return this.characterCount > this.maxChars;
    },
  },
  methods: {
    updateCharacterCount() {
      if (this.inputText.length > this.maxChars) {
        this.inputText = this.inputText.slice(0, this.maxChars);
      }
    },
  },
};
</script>
