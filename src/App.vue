<template>
  
    <div class="container my-5">
      <h1 class="bg-success p-2 text-white text-center">เลือกสินค้าใส่ offcanvas</h1>
      <hr />

      <div class="row justify-content-sm-center mt-4">
        <div class="col-md-3 col-sm-6 col-xs-12 my-3" v-for="ca in pro" :key="ca.id">
          <div class="card" style="width: 15rem">
            <img :src="ca.img" class="card-img-top" />
            <div align="center" class="card-body">
              <h5 class="card-title">{{ ca.name }}</h5>
              <p class="card-text">{{ ca.pri }}</p>

              <input
                class="form-check-input"
                type="checkbox"
                :value="ca"
                v-model="cart"
              />
            </div>
          </div>
        </div>
        <div
          class="offcanvas offcanvas-end p-3 bg-success bg-opacity-60 text-white"
          tabindex="-1"
          id="offcanvasRight"
          data-bs-backdrop="false"
        >
          <div class="offcanvas-header">
            <h5>รายการสินค้าในรถเข็น</h5>
            <button
              type="button"
              class="btn-close text-reset"
              data-bs-dismiss="offcanvas"
            ></button>
          </div>
          <div class="offcanvas-body">
            <div v-if="cart.length == 0">ไม่มีสินค้าในรถเข็น</div>
            <div v-else>
              <!-- ถ้ามีสินค้าใน (อาร์เรย์) รถเข็น ให้แสดงรายการแบบลิสต์ -->
              <ul>
                <li v-for="item in cart" :key="item">{{ item.name }}</li>
              </ul>

              <!-- ปุ่มสำหรับยกเลิกสินค้าทั้งหมดในรถเข็น โดยการลบข้อมูลในอาร์เรย์ -->
              <button class="btn btn-danger d-block my-4" @click="cart = []">
                ลบทั้งหมด
              </button>

              <!-- แนวทางการใช้ Checkbox อันเดียว เพื่อกำหนดสถานะ -->
              <div class="form-check mb-2">
                <input
                  type="checkbox"
                  class="form-check-input"
                  v-model="confirmCart"
                />
                <label for="chkConfirmCart" class="form-label mb-1"
                  >ยืนยันสินค้าในรถเข็น</label
                >
              </div>
              <button  class="btn btn-sm btn-primary" :disabled="!confirmCart">
                ไปต่อ
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="row justify-content-center">
      <button 
        class="btn btn-success my-3"
        data-bs-toggle="offcanvas"
        data-bs-target="#offcanvasRight"
      >
        สำรวจรถเข็น
      </button>
    </div>
    </div>
  
</template>
<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      confirmCart: false,
      cart: [],
      pro: [
        {
          id: 1,
          name: "ข้าว1",
          img: "https://media.istockphoto.com/id/1204220334/th/%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B8%96%E0%B9%88%E0%B8%B2%E0%B8%A2/%E0%B9%84%E0%B8%81%E0%B9%88%E0%B8%9B%E0%B8%A3%E0%B8%B8%E0%B8%87%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2%E0%B8%8B%E0%B8%AD%E0%B8%AA%E0%B9%81%E0%B8%81%E0%B8%87%E0%B8%81%E0%B8%B0%E0%B8%AB%E0%B8%A3%E0%B8%B5%E0%B9%88.jpg?s=612x612&w=0&k=20&c=UdAqPY_YTxlVw5nQDu1cXb6UU0NzQLTO-DDe217IlDE=",
          pri: "ราคา 50 บาท",
          re: false,
        },
        {
          id: 2,
          name: "ข้าว2",
          img: "https://media.istockphoto.com/id/1438085655/th/%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B8%96%E0%B9%88%E0%B8%B2%E0%B8%A2/%E0%B9%81%E0%B8%81%E0%B8%87%E0%B8%81%E0%B8%B0%E0%B8%AB%E0%B8%A3%E0%B8%B5%E0%B9%88%E0%B9%84%E0%B8%81%E0%B9%88%E0%B9%84%E0%B8%97%E0%B8%A2%E0%B9%81%E0%B8%A5%E0%B8%B0%E0%B8%96%E0%B8%B1%E0%B9%88%E0%B8%A7%E0%B8%A5%E0%B8%B4%E0%B8%AA%E0%B8%87%E0%B8%81%E0%B8%B1%E0%B8%9A%E0%B8%82%E0%B9%89%E0%B8%B2%E0%B8%A7%E0%B9%83%E0%B8%99%E0%B8%8A%E0%B8%B2%E0%B8%A1%E0%B8%AA%E0%B8%B5%E0%B9%80%E0%B8%97%E0%B8%B2%E0%B8%9E%E0%B8%B7%E0%B9%89%E0%B8%99%E0%B8%AB%E0%B8%A5%E0%B8%B1%E0%B8%87%E0%B8%AA%E0%B8%B5%E0%B9%80%E0%B8%82%E0%B9%89%E0%B8%A1.jpg?s=612x612&w=0&k=20&c=LbhyWBqc-P6dQU1K4gmoVL5wNc_tctvzCmKCRxFtIC8=",
          pri: "ราคา 70 บาท",
          re: false,
        },
        {
          id: 3,
          name: "ข้าว3",
          img: "https://media.istockphoto.com/id/1308781906/th/%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B8%96%E0%B9%88%E0%B8%B2%E0%B8%A2/%E0%B9%84%E0%B8%81%E0%B9%88%E0%B9%81%E0%B8%81%E0%B8%87%E0%B8%81%E0%B8%B0%E0%B8%97%E0%B8%B4%E0%B8%A1%E0%B8%B0%E0%B8%A1%E0%B9%88%E0%B8%A7%E0%B8%87.jpg?s=612x612&w=0&k=20&c=o6h_412oLd3NEfNNNtIMEtHVRUST0ai_ttyj_03P2Tk=",
          pri: "ราคา 60 บาท",
          re: false,
        },
        {
          id: 4,
          name: "ข้าว4",
          img: "https://media.istockphoto.com/id/1290127679/th/%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B8%96%E0%B9%88%E0%B8%B2%E0%B8%A2/%E0%B8%8A%E0%B8%B2%E0%B8%A1%E0%B9%84%E0%B8%81%E0%B9%88%E0%B9%80%E0%B8%81%E0%B9%87%E0%B8%9A%E0%B9%80%E0%B8%81%E0%B8%B5%E0%B9%88%E0%B8%A2%E0%B8%A7.jpg?s=612x612&w=0&k=20&c=8GW5DIUwdmDx167MqsiJca5_abAkwO475RwBMk8Sz0k=",
          pri: "ราคา 150 บาท",
          re: false,
        },
        {
          id: 5,
          name: "ข้าว5",
          img: "https://media.istockphoto.com/id/1132762109/th/%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B8%96%E0%B9%88%E0%B8%B2%E0%B8%A2/%E0%B8%82%E0%B9%89%E0%B8%B2%E0%B8%A7%E0%B8%82%E0%B8%B2%E0%B8%A7-b-%E0%B8%8A%E0%B8%B4%E0%B9%89%E0%B8%99%E0%B9%84%E0%B8%81%E0%B9%88%E0%B9%81%E0%B8%A5%E0%B8%B0%E0%B8%81%E0%B8%B0%E0%B8%AB%E0%B8%A5%E0%B9%88%E0%B9%8D%E0%B8%B2%E0%B8%9B%E0%B8%A5%E0%B8%B5-%E0%B8%AD%E0%B8%B2%E0%B8%AB%E0%B8%B2%E0%B8%A3%E0%B8%8D%E0%B8%B5%E0%B9%88%E0%B8%9B%E0%B8%B8%E0%B9%88%E0%B8%99.jpg?s=612x612&w=0&k=20&c=eGnkByjsocFUZrPPM_w8a_l0m-VwZV11dkLo49kTx3g=",
          pri: "ราคา 100 บาท",
          re: false,
        },
        {
          id: 6,
          name: "ข้าว6",
          img: "https://media.istockphoto.com/id/823764178/th/%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B8%96%E0%B9%88%E0%B8%B2%E0%B8%A2/%E0%B8%81%E0%B8%B0%E0%B8%AB%E0%B8%A5%E0%B9%88%E0%B9%8D%E0%B8%B2%E0%B8%9B%E0%B8%A5%E0%B8%B5%E0%B8%95%E0%B8%B8%E0%B9%8B%E0%B8%99%E0%B8%AB%E0%B8%A3%E0%B8%B7%E0%B8%AD%E0%B8%95%E0%B8%B8%E0%B9%8B%E0%B8%99%E0%B8%81%E0%B8%B0%E0%B8%AB%E0%B8%A5%E0%B9%88%E0%B9%8D%E0%B8%B2%E0%B8%9B%E0%B8%A5%E0%B8%B5%E0%B8%81%E0%B8%B0%E0%B8%AB%E0%B8%A5%E0%B9%88%E0%B9%8D%E0%B8%B2%E0%B8%9B%E0%B8%A5%E0%B8%B5%E0%B8%81%E0%B8%B0%E0%B8%AB%E0%B8%A5%E0%B9%88%E0%B9%8D%E0%B8%B2%E0%B8%9B%E0%B8%A5%E0%B8%B5.jpg?s=612x612&w=0&k=20&c=CGEoNCXQKvBTrS9O2dBHmTPT-65Y4un8MixUC_rPfM4=",
          pri: "ราคา 95 บาท",
          re: false,
        },
        {
          id: 7,
          name: "ข้าว7",
          img: "https://media.istockphoto.com/id/1421270958/th/%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B8%96%E0%B9%88%E0%B8%B2%E0%B8%A2/dal-khichadi-%E0%B8%AB%E0%B8%A3%E0%B8%B7%E0%B8%AD-masala-khichdi-%E0%B9%80%E0%B8%9B%E0%B9%87%E0%B8%99%E0%B8%AA%E0%B8%B9%E0%B8%95%E0%B8%A3%E0%B8%AD%E0%B8%B4%E0%B8%99%E0%B9%80%E0%B8%94%E0%B8%B5%E0%B8%A2%E0%B9%81%E0%B8%AA%E0%B8%99%E0%B8%AD%E0%B8%A3%E0%B9%88%E0%B8%AD%E0%B8%A2%E0%B8%97%E0%B8%B5%E0%B9%88%E0%B8%97%E0%B9%8D%E0%B8%B2%E0%B8%88%E0%B8%B2%E0%B8%81%E0%B8%96%E0%B8%B1%E0%B9%88%E0%B8%A7%E0%B8%9D%E0%B8%B1%E0%B8%81%E0%B8%A2%E0%B8%B2%E0%B8%A7%E0%B8%9C%E0%B8%AA%E0%B8%A1.jpg?s=612x612&w=0&k=20&c=Ch8UejmCEuOzC4bkVRV1CDz3h2pC0rbB7-nLCs7CKJg=",
          pri: "ราคา 36 บาท",
          re: false,
        },
        {
          id: 8,
          name: "ข้าว8",
          img: "https://media.istockphoto.com/id/1440548779/th/%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B8%96%E0%B9%88%E0%B8%B2%E0%B8%A2/%E0%B8%A1%E0%B8%B8%E0%B8%A1%E0%B8%A1%E0%B8%AD%E0%B8%87%E0%B8%94%E0%B9%89%E0%B8%B2%E0%B8%99%E0%B8%9A%E0%B8%99%E0%B8%82%E0%B8%AD%E0%B8%87%E0%B8%AD%E0%B8%B2%E0%B8%AB%E0%B8%B2%E0%B8%A3%E0%B9%81%E0%B8%81%E0%B8%B0%E0%B8%A3%E0%B8%AA%E0%B9%80%E0%B8%9C%E0%B9%87%E0%B8%94%E0%B9%81%E0%B8%9A%E0%B8%9A%E0%B8%AD%E0%B8%B4%E0%B8%99%E0%B9%80%E0%B8%94%E0%B8%B5%E0%B8%A2%E0%B8%94%E0%B8%B1%E0%B9%89%E0%B8%87%E0%B9%80%E0%B8%94%E0%B8%B4%E0%B8%A1%E0%B8%9E%E0%B8%A3%E0%B9%89%E0%B8%AD%E0%B8%A1%E0%B8%82%E0%B9%89%E0%B8%B2%E0%B8%A7%E0%B8%9A%E0%B8%B2%E0%B8%AA%E0%B8%A1%E0%B8%B2%E0%B8%95%E0%B8%B4%E0%B9%83%E0%B8%99%E0%B8%8A%E0%B8%B2%E0%B8%A1.jpg?s=612x612&w=0&k=20&c=jfVaH_tOL0LVaJ6itAHvXrTFLUj5VrgwUR3qihBWn64=",
          pri: "ราคา 169 บาท",
          re: false,
        },
      ],
    };
  },
};
</script>

