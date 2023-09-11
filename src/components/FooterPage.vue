<template>
  <footer class="footer-section">
    <div class="overlay"></div>
    <div class="footer-content">
      <h3 class="font-Bold pt-5">لا تتردد في التواصل معنا</h3>
      <p  class="py-2 font-Regular">شاركنا اللحظات الجميلة وكون جزء من عيلتنا</p>
      <div class="d-flex justify-content-around ">
        <input
          type="text"
          class="form-control w-size"
          id="exampleInputName"
          aria-describedby="emailHelp"
          placeholder="سجل بإيميلك وكون على اطلاع بكل جديد"
        />
        <button type="button" class="btn btn-light">إشترك الآن</button>
      </div>
      <div class="box-bottom " >
        <p class="font-Regular"> 
          للراغبين في إضافة فعالياتهم إلى المنصة الرجاء التواصل عن طريق البريد
          الإلكتروني
        </p>
        <p class="font-Regular">Techshef@gmail.com</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "FooterSection",
};
</script>

<style scoped>
.footer-section {
  position: relative;
  background-image: url("../assets/bg-footer2.png");
  background-size: cover;
  background-position: center;
  color: white;
  text-align: center;
  padding: 20px 0;
  height: 450px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.footer-content{
  width: 37%;
}
.w-size{
    width: 80%;
    padding: 10px;
}

.box-bottom{
    padding-top: 60px;
}
</style>