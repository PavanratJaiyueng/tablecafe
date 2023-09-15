<script setup>
//import...
import { ref, reactive , computed} from 'vue';


//ตัวแปร
const travelList=ref([
  { name :'Tha Chang Cafe' , price: 200 , size:{s:200,m:150,l:200}, img:"https://scontent.fbkk22-2.fna.fbcdn.net/v/t1.15752-9/373465087_984092232809851_4847077767634925902_n.jpg?_nc_cat=106&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeGioVpRR3WJUZKK2jhoTuxZRP8-1rH8BHFE_z7WsfwEcRriaIcPcwHL72Zx9mqu_5BA3zSGjacpPtgZNzWvoYj5&_nc_ohc=GfUD5XnV0C4AX9W1cSV&_nc_ht=scontent.fbkk22-2.fna&oh=03_AdQhUjWHGrswAzbbh1gYNYpjiF9Qm6Nwit-H9OJhxOJXZQ&oe=652B5278", quantity: 0 },
  { name :'Overnight' , price: 100, size:{s:100,m:180,l:250}, img:"https://scontent.fbkk22-3.fna.fbcdn.net/v/t1.15752-9/376371735_1053530595636865_8305132071341148549_n.jpg?_nc_cat=111&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeHGU9NzjgZBtz4z5lfplBGfJhBvdDmc83wmEG90OZzzfEEUkCK5GRmdwE7G2iv2515xnCtClyab_OhsrDtEWXmb&_nc_ohc=EGCndsbxhH0AX8hLDJe&_nc_ht=scontent.fbkk22-3.fna&oh=03_AdRd5NgzyVdPsLZQwGTpbtaw8O1F3CafkjUrJNDn9Bu2nA&oe=652B50A3", quantity: 0 } ,
  { name :'Sunthararom', price: 100,  size:{s:100,m:190,l:300}, img:"https://scontent.fbkk22-2.fna.fbcdn.net/v/t1.15752-9/375236315_3473646946283174_4808726927424589164_n.jpg?_nc_cat=105&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeHEYceiewhwHBhfGU_wF0DS3nQ9XNSzGmTedD1c1LMaZFpvfs0KA-rDpLOGaUKTmfqJuasmDkXM6bM1TcKJ_d9v&_nc_ohc=TM3WW_3B7TsAX9bvKMv&_nc_ht=scontent.fbkk22-2.fna&oh=03_AdRg_lD0InUs1VD9M3NLcpoxjjWZ1zBk_EBep9JyegbkQg&oe=652B4C17", quantity: 0 } ,
  { name :'The Good view', price: 150 ,  size:{s:150,m:200,l:500}, img:"https://scontent.fbkk22-4.fna.fbcdn.net/v/t1.15752-9/279960778_2657755434357496_5443268689653912444_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeFAtR7RwLk_q3RfDljYHyH9JubGDiUW1i0m5sYOJRbWLWmPIQAKt9WtpBGWUu3p6C-GxAIYjMGBH30pRjSxAFFy&_nc_ohc=Sp0K1NCo5cwAX-sNe-m&_nc_ht=scontent.fbkk22-4.fna&oh=03_AdS3x4b0gZeZstc4EIXOvVJyC2hIoKzA69PgEBx7c4s4Zg&oe=652B581B", quantity: 0 },
  { name :'Tawandang', price: 190 ,  size:{s:190,m:250,l:700}, img:"https://scontent.fbkk22-6.fna.fbcdn.net/v/t1.15752-9/377095120_210868785114352_4424798731387928204_n.jpg?_nc_cat=104&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeH0m_KdUaycx6Hv6t-vBPRXuw-xhY7n7lq7D7GFjufuWtMVjPNMlzLX6iJqzT08z8ezWmvdt643tA_tfa5muO50&_nc_ohc=XdIsS5rZVG0AX9rKyi6&_nc_ht=scontent.fbkk22-6.fna&oh=03_AdSEU1itls_gB8zBF5lJ1g9spmllKLaElyvzASUyViMLyw&oe=652B380F", quantity: 0 },
  { name :'Bangkwang   ', price: 140 ,  size:{s:140,m:130,l:650}, img:"https://scontent.fbkk22-8.fna.fbcdn.net/v/t1.15752-9/377100842_1012755073397859_5236617005665812726_n.jpg?_nc_cat=110&ccb=1-7&_nc_sid=ae9488&_nc_eui2=AeEFOMBrGsAGTGwlXGHFnsFvU2jNX4DXRntTaM1fgNdGe4U7BXSb3_CzsHZ57IPFsswo84dmQpIIwovGExOBmFVH&_nc_ohc=VEwBjiKpfNMAX-ogsSl&_nc_ht=scontent.fbkk22-8.fna&oh=03_AdSrevDouzi7KNyO2ZWzRTflMFIgT64ZVGG3kmlVTmctrw&oe=652B322A", quantity: 0 }
  
]);

// เก็บข้อมูลการจองร้าน
const bookingList = reactive([]);



const totalAmount = computed(() => {
  return bookingList.reduce((total, item) => total + item.price, 0);
});


//function

function booking_control(name, quantity) {
  const itemindex = bookingList.findIndex(item => item.name === name);

  if (itemindex !== -1) {
    bookingList[itemindex].quantity += quantity;
    bookingList[itemindex].price = bookingList[itemindex].quantity * travelList.value.find(item => item.name === name).price;
  } else {
    const item = {
      name: name,
      quantity: quantity,
      price: quantity * travelList.value.find(item => item.name === name).price
    };
    bookingList.push(item);
  }
}

function quantity_increased(item) {
  item.quantity++;
  item.price = item.quantity * travelList.value.find(travel => travel.name === item.name).price;
}

function quantity_decreased(item) {
  if (item.quantity > 0) {
    item.quantity--;
    item.price = item.quantity * travelList.value.find(travel => travel.name === item.name).price;
  }
}

function removeItem(index) {
  bookingList.splice(index, 1);
}

//pop up

const form_costumer = ref({
  name: "",
  phone: "",
  date: "",
  time: ""
});

const showPopup = ref(false);

function togglePopup() {
  showPopup.value = !showPopup.value;
}

const isFormComplete = ref(false);

function checkFormCompletion() {
  const { name, phone, date, time } = form_costumer;
  isFormComplete.value = name !== "" && phone !== "" && date !== "" && time !== "";
}


</script>

<template>

    <div class="container">
      <div class="row">
        <div class="col" v-for=" (i,index) in travelList" :key="index">
          <div class="card shadow">
            <div class="bd-placeholder-img card-img-top" width="100%" height="225"  >
              <title>Placeholder</title>
              <img :src="i.img" height="300" width="300">
              <rect width="100%" height="100%" fill="#55595c" />
            </div>
            <div class="card-body">
              <h5 class="card-title">{{ i.name }}</h5>
                <p>ราคาโต๊ะ ={{i.size.s}}</p>
                <h>**** 6 คนต่อ 1 โต๊ะ ****</h>
                <p class="card-text">จำนวนโต๊ะ <br>
                   <input type="number" class="value_out" v-model="i.quantity">
                </p>
              <div class="box_btn">
                <div class="btn-group">
                  <button type="button" class="btn btn-sm btn-outline-secondary">View</button>
                  <button type="button" class="btn btn-sm btn-outline-secondary" @click="booking_control(i.name,i.quantity)">จองโต๊ะ</button>
                </div>
              </div>
            </div>
          </div>
        </div>
    </div>
  </div>

  <div class="contrainer_costumer " v-if="bookingList.length>0">
  <div class="form_box"> <h2 style="text-align: center;">กรุณากรอกข้อมูล</h2></div>
  <form>
    <div class="form_box">
      <label for="name">Name </label><br>
      <input type="text" id="name" class="form-control" v-model="form_costumer.name" required @input="checkFormCompletion">
    </div>
    <div class="form_box">
      <label for="phone">Tel. </label><br>
      <input type="tel" id="phone" class="form-control" v-model="form_costumer.phone" required @input="checkFormCompletion">
    </div>
    <div class="form_box">
      <label for="date">Date </label><br>
      <input type="date" id="date" class="form-control" v-model="form_costumer.date" required @input="checkFormCompletion">
    </div>
    <div class="form_box">
      <label for="time">Time</label><br>
      <input type="time" id="time" class="form-control" v-model="form_costumer.time" required @input="checkFormCompletion">
    </div>
    <div class="form_box">
      <button type="button" class="btn btn-success" @click="togglePopup" :disabled="!isFormComplete">บันทึกการจอง</button>
    </div>
  </form>
</div>

      <h1 style="text-align: center;" v-if="bookingList.length>0" class="head">รายการจองโต๊ะ</h1>
      <div class="List_cout">
        <table class="table table-hover" v-if="bookingList.length>0">
          <table class="table">
            <thead>
              <tr>
                <th scope="col">ลำดับ</th>
                <th scope="col">ชื่อร้าน</th>
                <th scope="col">จำนวนโต๊ะ</th>
                <th scope="col">ราคา</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(i,index) in bookingList" :key="index" >
                <th scope="row">{{index+1}}</th>
                <td>{{ i.name }}</td>
                <td>
                    <div class="table_quantity">
                        <button type="button" class="add" @click="quantity_increased(i)" >+</button>
                        <span>{{ i.quantity }}</span>
                        <button type="button" class="cut"  @click="quantity_decreased(i)" :end="i.quantity === 0">-</button>
                    </div>
                </td>
                <td>{{ i.price }}</td>
                <td>
                    <button type="button" class="btn btn-danger" @click="removeItem(index)" >ลบ</button>
                </td>
              </tr>
            </tbody>
          </table>
        </table>
      </div>
      
    
<div v-if="showPopup" class="overlay">
  <div class="popup">
    <h2 style="text-align: center; color:green;">ยืนยันการจองสำเร็จ</h2>
    <h3>รายละเอียด</h3>
    <div class="form">
      <strong>Name:</strong> {{ form_costumer.name }}
      <strong>Tel.:</strong> {{ form_costumer.phone }}
      <strong>Date:</strong> {{ form_costumer.date }}
      <strong>Time:</strong> {{ form_costumer.time }}
    </div>

    <table class="box_table">
      <thead>
        <tr>
          <th>ลำดับ</th>
          <th>ชื่อร้าน</th>
          <th>จำนวนโต๊ะ</th>
          <th>ราคา</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in bookingList" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.quantity }}</td>
          <td>{{ item.price }}</td>
        </tr>
      </tbody>
    </table>

    <div class="total_all">
    <strong>Total:</strong> {{ totalAmount }} Baht
    </div>

    <button class="btn btn-danger" @click="showPopup = false">ปิด</button>
  </div>
</div>



</template>
      


<style>
body {
  font-family: Arial, sans-serif;
  background-color: #006699;
}
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 20px auto;
  max-width: 1200px;
}
.card {
  background-color: #99CCCC;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  margin-bottom: 50px;
}
.card-title {
  font-size: 1.2rem;
  margin: 10px 0;
}

.card-text {
  font-size: 0.9rem;
}

.value_out {
  background-color: #DCDCDC;
  color:black;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 40px; /* ปรับขนาดความกว้างของ input */
  text-align: center; /* จัดข้อความตรงกลาง */
  font-size: 1rem;
}

.btn-group button {
  cursor: pointer;
}

.btn-group button {
  cursor: pointer;
}

.head {
  text-align: center;
  margin-top: 20px;
  font-size: 1.5rem;
}

.List_cout {
  margin-top: 20px;
}

.table_quantity {
  display: flex;
  align-items: center;
  justify-content: space-between; /* เพิ่มระยะห่างระหว่างองค์ประกอบ */
}

.add,
.cut {
  width: 30px;
  height: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color:#FFF0F5;
  color:#CD5C5C;
  border: none;
  cursor: pointer;
  font-size: 1rem;
  border-radius: 30%;
  margin-right: 20%; /* เพิ่มระยะห่างขวา */
  margin-left: 20%;  /* เพิ่มระยะห่างซ้าย */
}

.add:hover,
.cut:hover {
  background-color: rgb(128, 128, 128);

}

.contrainer_costumer {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

.form_box {
  margin-bottom: 15px;
}

.form-control {
  width: 100%;
  padding: 10px;
  border: 1px solid #D3D3D3;
  border-radius: 5px;
}

.btn-success {
  background-color: #28a745;
  color: #fff;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  font-size: 1rem;
  border-radius: 5px;
}

.btn-success:hover {
  background-color: #1d8c3b;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
}

.popup {
  max-width: 750px;
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}

.popup h2 {
  text-align: center;
  color: green;
  margin-bottom: 10px;
}

.popup h3 {
  margin-top: 10px;
}

.popup .form strong {
  display: block;
  margin-top: 10px;
}

.box_table {
  width: 100%;
  margin-top: 20px;
}

.popup button {
  background-color: #dc3545;
  color: #fff;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  font-size: 1rem;
  border-radius: 5px;
  margin-top: 10px;
}

.popup button:hover {
  background-color: #c82333;
}


.contrainer_costumer {
  width: 380px; 
  height: 100%; 
  margin: 10px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  background-color: #E6E6FA;
  float: right; /* เพิ่ม float: right; เพื่อจัดองค์ประกอบทางขวา */
}

.table {
  width: 100%; /* ตารางที่มีความกว้างเต็มหน้าจอ */
  max-width: 800px; /* ตั้งค่าความกว้างสูงสุดของตาราง */
}




</style>