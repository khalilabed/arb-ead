<template>
  <div class="hero-section">
    <div class="container py-5">
      <div class="row d-flex align-items-center">
        <div class="col-md-12 col-lg-6 d-flex align-items-center">
          <div class="box-icon">
            <img src="../assets/sodi.png" alt="" />
          </div>
          <div class="top-resp">
            <h4 class="py-3 font-Medium">في ظلّ علم يعلو وطن ويزهو</h4>
            <p class="shadw font-Regular22">
              انضم إلى أجواء الفرح والفخر في احتفالاتنا <br />
              باليوم الوطني السعودي
            </p>
          </div>
        </div>
        <div class="col-md-12 col-lg-6">
          <p class="font-Medium24 text-rigth mr">
            ندعوك للاحتفال بتحقيق الأحلام
          </p>
          <div class="black">
            <p class="text-white size font-Medium16">
              وبهالمناسبة السعيدة قررنا نقدملك هدية بتقدر تستخدمها بتصميمك بتعبر
              عن محبتنا
            </p>
            <p class="text-light font-Regular14">
              سجل بإيميلك ورح نرسلك هدية تعجبك بإذن الله
            </p>
            <div class="row d-flex align-items-center justify-content-center">
              <div class="col-7">
                <form @submit.prevent="postData">
                  <div class="my-2">
                    <input
                      type="text"
                      class="form-control"
                      v-model="name"
                      placeholder="ادخل اسمك هنا"
                    />
                  </div>
                  <div class="my-2">
                    <input
                      type="email"
                      class="form-control"
                      v-model="email"
                      placeholder="ايميلك الشخصي"
                    />
                  </div>
                  <div class="my-2 but">
                    <button
                      type="submit"
                      class="btn btn-light font-Regular14 blod-none"
                    >
                      أطلب هديتك الفورية
                    </button>
                  </div>
                </form>
              </div>
              <div class="col-5">
                <div class="dds">
                  <img src="../assets/gift.png" alt="" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  methods: {
    async postData() {
      try {
        const response = await axios.post(
          "http://192.168.3.103/celebration/public/api/gifts",
          {
            name: this.name,
            email: this.email,
          }
        );
        console.log("Data sent successfully:", response.data);
        const newTab = window.open("https://google.com", "_blank");
        if (newTab) {
          newTab.focus(); // Optional: Focus on the new tab
        }
        this.name = "";
        this.email = "";
      } catch (error) {
        console.error("Error sending data:", error);
      }
    },
  },
};
</script>

<style>
@import "@/assets/css/styles.css";
</style>