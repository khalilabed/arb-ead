<template>
  <div>
    <!-- مصغرات الصور -->
    <div class="row">
      <div class="col-lg-3" v-for="(image, index) in images" :key="index">
        <img
          :src="image.src"
          :alt="image.alt"
          class="img-fluid"
          @click="selectImage(index)"
          :class="{ selected: selectedImageIndex === index }"
        />
      </div>
    </div>

    <!-- الكانفاس -->
    <canvas ref="canvas" width="600" height="500"></canvas>

    <!-- حقل إدخال النص -->
    <div class="py-4">
      <input
        v-model="inputText"
        @input="updateCharacterCount"
        class="custom-input"
        :class="{ exceeded: isExceeded }"
        placeholder="أدخل النص هنا"
      />
      <div :class="{ 'character-count': true, exceeded: isExceeded }">
        {{ characterCount }} / {{ maxChars }}
      </div>
    </div>

    <!-- زر تنزيل الصورة -->
    <button @click="downloadImage">تنزيل الصورة</button>

    <!-- شعار -->
    <div class="file-input py-5">
      <input type="file" @change="uploadLogo" accept="image/*" />
      <label class="file-input__label" for="file-input">
        <i class="fa-solid fa-cloud-arrow-up icon-size"></i>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedColor: "#000000",
      inputText: "",
      maxChars: 50,
      canvasContext: null,
      images: [
        {
          src: require("@/assets/prev2.png"), // تأكد من المسار الصحيح للصورة
          alt: "Image 1",
        },
        {
          src: require("@/assets/prev2.png"), // تأكد من المسار الصحيح للصورة
          alt: "Image 2",
        },
        {
          src: require("@/assets/prev2.png"), // تأكد من المسار الصحيح للصورة
          alt: "Image 3",
        },
        {
          src: require("@/assets/prev2.png"), // تأكد من المسار الصحيح للصورة
          alt: "Image 4",
        },
      ],
      selectedImageIndex: null, // الفهرس للصورة المحددة
      logo: null, // الشعار المحمل
    };
  },
  mounted() {
    this.canvasContext = this.$refs.canvas.getContext("2d");
  },
  computed: {
    characterCount() {
      return this.inputText.length;
    },
    isExceeded() {
      return this.characterCount > this.maxChars;
    },
  },
  watch: {
    // مراقبة التغييرات في النص والشعار
    inputText: "addTextAndLogoToImage",
    logo: "addTextAndLogoToImage",
  },
  methods: {
    updateCharacterCount() {
      if (this.inputText.length > this.maxChars) {
        this.inputText = this.inputText.slice(0, this.maxChars);
      }
    },
    // دالة لتحديد الصورة المختارة
    selectImage(index) {
      this.selectedImageIndex = index;

      if (this.selectedImageIndex !== null) {
        const selectedImageData = this.images[this.selectedImageIndex]; // معلومات الصورة المختارة
        const newSelectedImage = new Image();
        newSelectedImage.src = selectedImageData.src; // تعيين مسار الصورة

        newSelectedImage.onload = () => {
          this.canvasContext.clearRect(
            0,
            0,
            this.$refs.canvas.width,
            this.$refs.canvas.height
          );
          this.canvasContext.drawImage(
            newSelectedImage,
            0,
            0,
            this.$refs.canvas.width,
            this.$refs.canvas.height
          );
          this.addTextAndLogoToImage(); // إضافة النص والشعار بمجرد تحديد الصورة
        };
      }
    },
    // دالة لإضافة النص والشعار إلى الصورة
    // دالة لإضافة النص والشعار إلى الصورة
    addTextAndLogoToImage() {
      if (this.selectedImageIndex !== null) {
        const selectedImage = this.images[this.selectedImageIndex];
        const newSelectedImage = new Image();
        newSelectedImage.src = selectedImage.src;

        newSelectedImage.onload = () => {
          this.canvasContext.clearRect(
            0,
            0,
            this.$refs.canvas.width,
            this.$refs.canvas.height
          );
          this.canvasContext.drawImage(
            newSelectedImage,
            0,
            0,
            this.$refs.canvas.width,
            this.$refs.canvas.height
          );

          // قيمة ثابتة لموقع النص في الوسط الأفقي
          const x = this.$refs.canvas.width / 2;

          // موقع ثابت في الوسط الرأسي
          const y =
            this.$refs.canvas.height / 2 +
            parseInt(this.canvasContext.font) * 0.3;

          // رسم النص
          this.canvasContext.font = "20px Arial";
          this.canvasContext.fillStyle = this.selectedColor;
          this.canvasContext.textAlign = "center"; // توسيط النص أفقيًا
          this.canvasContext.fillText(this.inputText, x, y);

          // رسم الشعار إذا كان موجودًا
          if (this.logo) {
            this.canvasContext.drawImage(this.logo, 10, 10, 80, 80); // تعديل الأبعاد حسب رغبتك
          }
        };
      }
    },
    downloadImage() {
      if (this.$refs.canvas) {
        const canvas = this.$refs.canvas;
        const imageUrl = canvas.toDataURL("image/png");
        const link = document.createElement("a");
        link.href = imageUrl;
        link.download = "canvas_image.png";
        link.click();
      }
    },
    // دالة لرفع شعار
    uploadLogo(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.logo = new Image();
          this.logo.src = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    },
  },
};
</script>

<style>
/* أنماط CSS الخاصة بالكانفاس وحقل النص والشعار */
.custom-input {
  width: 100%;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-bottom: 10px;
}

.file-input {
  text-align: center;
  position: relative;
}

.file-input__label {
  display: block;
  background-color: #3498db;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.file-input__label i {
  margin-right: 5px;
}

.character-count {
  font-size: 14px;
  color: #777;
}

.exceeded {
  color: red;
}

/* إضافة الأسلوب للعنصر المحدد */
.selected {
  border: 2px solid #3498db;
}

/* أنماط CSS الخاصة بالكانفاس وحقل النص والشعار */
.custom-input {
  width: 100%;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-bottom: 10px;
}

.file-input {
  text-align: center;
  position: relative;
}

.file-input__label {
  display: block;
  background-color: #3498db;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.file-input__label i {
  margin-right: 5px;
}

.character-count {
  font-size: 14px;
  color: #777;
}

.exceeded {
  color: red;
}

/* إضافة الأسلوب للعنصر المحدد */
.selected {
  border: 2px solid #3498db;
}

.custom-textarea {
  width: 100%;
  height: 100px;
}
.character-count {
  margin-top: 10px;
}
.exceeded {
  color: red;
}
.icon-size {
  font-size: 24px;
}
.box-buttom button {
  background-color: #5fbc5f;
  border: none;
  padding: 10px;
}
.box-Previw {
  background-image: url("../assets/prew.png");
  background-repeat: no-repeat;
  background-size: 100% 100%;
}

.wit-img img {
  width: 320px;
  display: block;
  margin: 0 auto;
}

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

.choose img {
  width: 100%;
}
.squ,
.squ2,
.rect {
  padding: 6px 9px;
  background-color: #c0dd49;
  margin-left: 9px;
}
.squ2 {
  padding: 0px 17px;
}
.rect {
  padding: 0px 11px;
}
.tablinks {
  cursor: pointer;
}

.tablinks.active {
  border: 4px solid #c0dd49;
  border-radius: 15px;
}

.preview {
  margin-top: 20px;
  text-align: center;
}

.preview img {
  /* max-width: 28%; */
  max-height: 400px;
}
img {
  width: 100%;
}
.thumbnails .selected {
  border: 2px solid blue;
}

/* أسلوب التحديد للزر لإضافة النص */
button.add-text.selected {
  background-color: green;
  color: white;
}

.custom-textarea {
  width: 100%;
  height: 100px;
}
.character-count {
  margin-top: 10px;
}
.exceeded {
  color: red;
}
.icon-size {
  font-size: 24px;
}
</style>
