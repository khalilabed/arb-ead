<template>
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
      <img src="../assets/GroupReviw.png" alt="" />
    </div>
    <div>
      <div class="py-4 box-buttom">
        <button type="button" class="btn btn-success ms-3 px-4">
          <i class="fas fa-download ps-2"></i> تنزيل البطاقة على جهازك
        </button>
        <button type="button" class="btn btn-success px-4">
          <i class="fas fa-share-alt ps-2"></i>شارك البطاقة مع أصدقائك
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
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
/* img{
     width: 100%;
 } */
</style>