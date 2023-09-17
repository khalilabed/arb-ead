<template>
  <!-- The Start Sections Selects Choose -->
  <div class="text-center py-5">
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
      >1</span
    ><span class="font-Medium16 fw-normal"> اختار قالبك المفضل </span>
  </div>

  <!-- start section img 1 -->
  <div class="container">
    <p class="pt-5"><span class="rect"></span>مربع</p>
    <Carousel
      :itemsToShow="isMobile ? 1 : 3"
      :wrapAround="true"
      :transition="500"
    >
      <!-- الشرائح -->

      <Slide v-for="(image, index) in images.slice(0, 4)" :key="index">
        <div class="carousel__item">
          <div class="container">
            <div class="row">
              <div class="">
                <img
                  :src="image.src"
                  :alt="image.alt"
                  class="tablinks"
                  @click="selectImage(index)"
                  :class="{ selected: selectedImageIndex === index }"
                />
              </div>
            </div>
          </div>
        </div>
      </Slide>

      <template #addons>
        <navigation />
        <pagination />
      </template>
    </Carousel>
  </div>
  <!-- End section img 1 -->

  <!-- start section img 2 -->
  <div class="container">
    <p class="pt-5"><span class="squ"></span> مستطيل</p>
    <Carousel :itemsToShow="isMobile ? 1 : 3" :wrapAround="true" :transition="500">
      <!-- الشرائح -->
      <Slide v-for="(image, index) in images.slice(4, 7)" :key="index">
        <div class="carousel__item">
          <div class="container">
            <div class="row">
              <div class="">
                <img
                  :src="image.src"
                  :alt="image.alt"
                  class="tablinks"
                  @click="selectImage(index + 4)"
                  :class="{ selected: selectedImageIndex === index + 4 }"
                />
              </div>
            </div>
          </div>
        </div>
      </Slide>

      <template #addons>
        <navigation />
        <pagination />
      </template>
    </Carousel>
  </div>
  <!-- End section img 2 -->

  <!-- start section img 3 -->
  <div class="container">
    <p class="pt-5"><span class="squ2"></span> مستطيل</p>
    <Carousel :itemsToShow="isMobile ? 1 : 3" :wrapAround="true" :transition="500">
      <!-- الشرائح -->
      <Slide v-for="(image, index) in images.slice(7)" :key="index">
        <div class="carousel__item">
          <div class="container">
            <div class="row">
              <div class="">
                <img
                  :src="image.src"
                  :alt="image.alt"
                  class="tablinks"
                  @click="selectImage(index + 7)"
                  :class="{ selected: selectedImageIndex === index + 7 }"
                />
              </div>
            </div>
          </div>
        </div>
      </Slide>
      <template #addons>
        <navigation />
        <pagination />
      </template>
    </Carousel>
  </div>
  <!-- end section img 3 -->

  <!-- The End Sections Selects Choose -->

  <!-- the Start Sections UplodeLoge  -->
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
        "
        >2</span
      >
      <span class="font-Medium16 fw-normal"
        >قم بتحميل الشعار الخاص بك بصيغة PNG</span
      >
      <div>
        <div class="file-input py-5">
          <input
            @change="uploadLogo"
            accept="image/*"
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
      ><span class="font-Medium16 fw-normal">قم بكتابة عبارة التهنئة</span>
      <div class="py-4">
        <textarea
          v-model="inputText"
          @input="updateCharacterCount"
          class="custom-textarea"
          :class="{ exceeded: isExceeded }"
        >
        </textarea>
        <input
          type="color"
          id="colorPicker"
          v-model="selectedColor"
          style="display: none"
        />

        <div :class="{ 'character-count': true, exceeded: isExceeded }">
          {{ characterCount }} / {{ maxChars }}
          <div class="color-options d-flex justify-content-center py-3">
            <div
              v-for="(color, index) in colorOptions"
              :key="index"
              class="color-option"
              @click="selectColor(color)"
            >
              <div
                class="color-circle"
                :style="{ backgroundColor: color }"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- the End Sections UplodeLoge  -->

  <!--the Start Section PreviewPage-->
  <div class="text-center box-Previw">
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
      >4</span
    ><span class="font-Medium16 fw-normal">عاين بطاقتك وحملها فوراً </span>
    <div class="wit-img d-flex justify-content-center py-4">
      <div class="row">
        <div class="col-lg-12">
          <div class="preview">
            <canvas ref="canvas"></canvas>
            <img ref="previewImage" />
          </div>
        </div>
      </div>
    </div>
    <div>
      <div class="py-4 box-buttom">
        <button
          type="button"
          class="btn btn-success ms-3 size-button"
          @click="downloadImage"
        >
          <i class="fas fa-download ps-2"></i> تنزيل البطاقة على جهازك
        </button>
        <button
          type="button"
          class="btn btn-success size-button"
          @click="shareOnFacebook"
        >
          <i class="fas fa-share-alt ps-2"></i> شارك البطاقة مع أصدقائك
        </button>
      </div>
    </div>
  </div>
  <!--the End Section PreviewPage-->
</template>

<script>
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Pagination, Navigation } from "vue3-carousel";

export default {
  components: {
    Carousel,
    Pagination,
    Navigation,
    Slide,
  },
  data() {
    return {
      isMobile: window.innerWidth < 768,
      colorOptions: [
        "#FF0000",
        "#00FF00",
        "#0000FF",
        "#FFFF00",
        "#ffc346",
        "#800080",
        "#9f469d",
      ],
      selectedColor: "#000000",
      selectedImageIndex: null,
      inputText: "",
      maxChars: 50,
      canvasContext: null,
      images: [
        {
          src: require("@/assets/one-1.png"),
          alt: "Image 1",
        },
        {
          src: require("@/assets/one-2.png"),
          alt: "Image 2",
        },
        {
          src: require("@/assets/one-3.jpg"),
          alt: "Image 3",
        },
        {
          src: require("@/assets/one-4.jpg"),
          alt: "Image 4",
        },
        {
          src: require("@/assets/M1.jpg"),
          alt: "وصف الصورة 1",
        },
        {
          src: require("@/assets/M2.jpg"),
          alt: "وصف الصورة 2",
        },
        {
          src: require("@/assets/M3.jpg"),
          alt: "وصف الصورة 3",
        },
        {
          src: require("@/assets/three-1.jpg"),
          alt: "وصف الصورة 1",
        },
        {
          src: require("@/assets/three-2.jpg"),
          alt: "وصف الصورة 1",
        },
        {
          src: require("@/assets/three-3.jpg"),
          alt: "وصف الصورة 2",
        },
        {
          src: require("@/assets/three-4.jpg"),
          alt: "وصف الصورة 3",
        },
      ],
      logo: null, // الشعار المحمل
    };
  },
  mounted() {
    window.addEventListener("resize", this.updateIsMobile);
    this.canvasContext = this.$refs.canvas.getContext("2d");
    if (!this.canvasContext) {
      console.error("Failed to get 2D context for canvas.");
      return;
    }
    setInterval(this.drawImage, 500);
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
    updateIsMobile() {
      this.isMobile = window.innerWidth < 768;
    },
    async shareOnFacebook() {
      try {
        // تحضير البيانات
        const message = "نص المنشور";
        const imageUrl = "URL_OF_IMAGE_TO_SHARE";
        const accessToken = "YOUR_ACCESS_TOKEN";

        // الطلب إلى API Facebook
        const response = await this.$http.post(
          `https://graph.facebook.com/v13.0/me/photos?access_token=${accessToken}`,
          {
            url: imageUrl,
            caption: message,
          }
        );

        // الاستجابة بنجاح
        console.log("تم نشر المنشور على Facebook:", response.data);
      } catch (error) {
        // حدث خطأ أثناء النشر
        console.error("حدث خطأ أثناء نشر المنشور:", error);
      }
    },

    updateCharacterCount() {
      if (this.inputText.length > this.maxChars) {
        this.inputText = this.inputText.slice(0, this.maxChars);
      }
    },
    selectColor(color) {
      this.selectedColor = color;
      this.addTextAndLogoToImage(); // قم بإعادة تطبيق النص والشعار بمجرد تحديد لون جديد
    },
    selectImage(index) {
      this.selectedImageIndex = index;
      if (this.selectedImageIndex !== null) {
        const selectedImageData = this.images[this.selectedImageIndex];
        const newSelectedImage = new Image();
        newSelectedImage.src = selectedImageData.src;

        newSelectedImage.onload = () => {
          // زيادة الارتفاع الأقصى والعرض الأدنى للصورة (على سبيل المثال 600 بكسل في الارتفاع و 300 بكسل في العرض)
          const maxHeight = 550;
          const minWidth = 400;

          let imageWidth = newSelectedImage.width;
          let imageHeight = newSelectedImage.height;

          // التحقق من الارتفاع والعرض الأدنى وقم بتعديل حجم الصورة إذا كان ضروريًا
          if (imageHeight > maxHeight || imageWidth < minWidth) {
            const scaleHeight = maxHeight / imageHeight;
            const scaleWidth = minWidth / imageWidth;

            const scale = Math.max(scaleHeight, scaleWidth);

            imageWidth *= scale;
            imageHeight *= scale;
          }

          this.$refs.canvas.width = imageWidth;
          this.$refs.canvas.height = imageHeight;

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
            newSelectedImage.width,
            newSelectedImage.height,
            0,
            0,
            this.$refs.canvas.width,
            this.$refs.canvas.height
          );
          this.addTextAndLogoToImage();

          window.scrollTo({
            top: window.innerHeight * 3.5,
            behavior: "smooth",
          });
        };
      }
      console.clear();
    },

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
            newSelectedImage.width,
            newSelectedImage.height,
            0,
            0,
            this.$refs.canvas.width,
            this.$refs.canvas.height
          );

          // تعيين خصائص النص بناءً على اللون المختار ونمط الخط
          this.canvasContext.font = '30px "Sans Medium", Arial'; // حجم الخط ونمط الخط
          this.canvasContext.fillStyle = this.selectedColor; // تحديد لون النص

          // موقع ثابت في الوسط الأفقي
          const x = this.$refs.canvas.width / 2;
          // موقع ثابت في الوسط الرأسي
          let y = this.$refs.canvas.height / 2.8;

          // النص مع سرد (\n) ليظهر على عدة أسطر
          const textLines = this.inputText.split("\n");
          for (let i = 0; i < textLines.length; i++) {
            this.canvasContext.textAlign = "center"; // توسيط النص أفقيًا
            this.canvasContext.textBaseline = "top"; // تعيين قاعدة النص لتكون في أعلى السطر

            const text = textLines[i];
            const textWidth = this.canvasContext.measureText(text).width; // قياس طول النص

            // التحقق من طول النص ومقارنته بالحد الذي ترغب فيه
            if (textWidth <= this.$refs.canvas.width) {
              // إذا كان النص أقل من أو يساوي العرض الكلي للكانفاس
              this.canvasContext.fillText(text, x, y);
            } else {
              // إذا كان النص أطول من العرض الكلي للكانفاس
              // قم بتقسيمه إلى أجزاء صغيرة لتناسب العرض
              const maxTextWidth = this.$refs.canvas.width;
              let startIndex = 0;
              while (startIndex < text.length) {
                const remainingText = text.slice(startIndex);
                const fitLength = this.findFitTextLength(
                  remainingText,
                  maxTextWidth
                );
                const fittedText = remainingText.slice(0, fitLength);
                this.canvasContext.fillText(fittedText, x, y);
                y += 30; // زيادة قيمة y للانتقال إلى السطر التالي
                startIndex += fitLength;
              }
            }

            y += 30; // زيادة قيمة y للانتقال إلى السطر التالي
          }

          // رسم الشعار إذا كان موجودًا
          if (this.logo) {
            this.canvasContext.drawImage(this.logo, 18, 18, 85, 75); // تعديل الأبعاد حسب رغبتك
          }
        };
      }
    },

    findFitTextLength(text, maxWidth) {
      let startIndex = 0;
      let endIndex = text.length;
      while (startIndex < endIndex) {
        const middleIndex = Math.floor((startIndex + endIndex) / 2);
        const middleText = text.slice(0, middleIndex);
        const middleTextWidth = this.canvasContext.measureText(middleText)
          .width;
        if (middleTextWidth <= maxWidth) {
          startIndex = middleIndex + 1;
        } else {
          endIndex = middleIndex;
        }
      }
      return startIndex;
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
@import "@/assets/css/styles.css";
img {
  border-radius: 8px;
}
img {
  width: 100%;
}
</style>
