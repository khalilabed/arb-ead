<template>
  <!-- The Start Sections Selects Choose -->
  <div class="container choose">
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
      >اختار قالبك المفضل
    </div>
    <div class="row">
      <p class=""><span class="rect"></span>مربع</p>
      <div class="col-lg-3" v-for="(image, index) in images1" :key="index">
        <img
          v-if="image"
          :src="image.src"
          :alt="image.alt"
          class="tablinks"
          @click="openTab(index, 'images1')"
          :class="{
            active:
              activeTab.section === 'images1' && activeTab.index === index,
          }"
        />
      </div>

      <div class="pt-5">
        <p class=""><span class="squ2"></span> مستطيل</p>
      </div>
      <div class="row">
        <div class="col-lg-4" v-for="(image, index) in images2" :key="index">
          <img
            v-if="image"
            :src="image.src"
            :alt="image.alt"
            class="tablinks"
            @click="openTab(index, 'images2')"
            :class="{
              active:
                activeTab.section === 'images2' && activeTab.index === index,
            }"
          />
        </div>
      </div>

      <div class="pt-5">
        <p class=""><span class="squ"></span> مستطيل</p>
      </div>
      <div class="row">
        <div class="col-lg-3" v-for="(image, index) in images3" :key="index">
          <img
            v-if="image"
            :src="image.src"
            :alt="image.alt"
            class="tablinks"
            @click="openTab(index, 'images3')"
            :class="{
              active:
                activeTab.section === 'images3' && activeTab.index === index,
            }"
          />
        </div>
      </div>
    </div>
  </div>
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
    >عاين بطاقتك وحملها فوراً
    <div class="wit-img d-flex justify-content-center py-4">
      <div class="row">
        <div class="col-lg-12">
          <div class="preview">
            <img
              v-if="activeImage"
              :src="activeImage.src"
              :alt="activeImage.alt"
            />
          </div>
        </div>
      </div>
    </div>
    <div>
      <div class="py-4 box-buttom">
        <button
          type="button"
          class="btn btn-success ms-3 px-4"
          @click="downloadCard"
        >
          <i class="fas fa-download ps-2"></i> تنزيل البطاقة على جهازك
        </button>
        <button type="button" class="btn btn-success px-4">
          <i class="fas fa-share-alt ps-2"></i>شارك البطاقة مع أصدقائك
        </button>
      </div>
    </div>
  </div>
  <!--the End Section PreviewPage-->
</template>

<style>
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
</style>

<script>
import html2canvas from "html2canvas";

export default {
  data() {
    return {
      inputText: "",
      maxChars: 24,
      images1: [
        {
          src: require("../assets/prev2.png"),
          alt: "Image 1",
        },
        {
          src: require("../assets/prev2.png"),
          alt: "Image 2",
        },
        {
          src: require("../assets/prev2.png"),
          alt: "Image 3",
        },
        {
          src: require("../assets/prev2.png"),
          alt: "Image 4",
        },
      ],
      images2: [
        {
          src: require("../assets/mostatel.png"),
          alt: "Image 5",
        },
        {
          src: require("../assets/mostatel.png"),
          alt: "Image 6",
        },
        {
          src: require("../assets/mostatel.png"),
          alt: "Image 7",
        },
      ],
      images3: [
        {
          src: require("../assets/hig.png"),
          alt: "Image 8",
        },
        {
          src: require("../assets/hig.png"),
          alt: "Image 9",
        },
        {
          src: require("../assets/hig.png"),
          alt: "Image 10",
        },
        {
          src: require("../assets/hig.png"),
          alt: "Image 11",
        },
      ],
      activeTab: { section: "", index: null },
    };
  },
  computed: {
    characterCount() {
      return this.inputText.length;
    },
    isExceeded() {
      return this.characterCount > this.maxChars;
    },
    activeImage() {
      // استخدم ال activeTab لعرض الصورة المختارة
      if (this.activeTab.section === "images1") {
        return this.images1[this.activeTab.index];
      } else if (this.activeTab.section === "images2") {
        return this.images2[this.activeTab.index];
      } else if (this.activeTab.section === "images3") {
        return this.images3[this.activeTab.index];
      }
      return null;
    },
  },
  methods: {
    openTab(index, section) {
      // تحديث العلامة التبويبية النشطة عند النقر على صورة
      this.activeTab = { section, index };
    },
    updateCharacterCount() {
      if (this.inputText.length > this.maxChars) {
        this.inputText = this.inputText.slice(0, this.maxChars);
      }
    },

    async downloadCard() {
      const imageElement = this.$refs.previewImage; // الحصول على الصورة من المعاينة
      if (imageElement) {
        const canvas = await html2canvas(imageElement);
        const imgData = canvas.toDataURL("image/png");

        // تنزيل الصورة كملف
        const link = document.createElement("a");
        link.download = "card.png";
        link.href = imgData;
        link.click();
      }
    },
  },
};
</script>
