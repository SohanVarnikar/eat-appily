<template>
  <div class="main">
    <header>
      <div class="tab">
        <img class="logo" src="../../src/assets/logo.png" alt="logo">
        <button class="tab-button" v-on:click="showAll"><strong>All ({{orders.length}})</strong></button>
        <button class="tab-button" v-on:click="getNewOrders"><strong>New ({{newOrders}})</strong></button>
        <button class="tab-button" v-on:click="getPreparingOrders"><strong>Preparing ({{preparing}})</strong></button>
        <button class="tab-button" v-on:click="getReadyOrders"><strong>Ready ({{ready}})</strong></button>
      </div>
    </header>
    <div class="row">
      <Order v-for="order in filteredOrders" :key="order.id" :order="order" @onStatusChange="onStatusChange" />
    </div>
  </div>
</template>

<script>
import OrderCard from "../components/OrderCard";
export default {
  components: {
    Order: OrderCard
  },
  data() {
    return { orders: [], filteredOrders: [] };
  },
  computed: {
    newOrders() {
      var orderCount = 0;
      orderCount = this.orders.filter(
        order => order.orderstatus == "Order Recived"
      ).length;
      return orderCount;
    },
    preparing() {
      var orderCount = 0;
      orderCount = this.orders.filter(
        order => order.orderstatus == "Prepareing"
      ).length;
      return orderCount;
    },
    ready() {
      var orderCount = 0;
      orderCount = this.orders.filter(
        order => order.orderstatus == "Ready to serve"
      ).length;
      return orderCount;
    }
  },
  created() {
    this.orders.push({
      orderId: "1",
      mobile: "9889734525",
      customerName: "Sohan",
      noOfItemsOrdered: 2,
      totalAmount: 250,
      orderstatus: "Order Recived"
    });
    this.orders.push({
      orderId: "11",
      mobile: "8889734525",
      customerName: "Rangs",
      noOfItemsOrdered: 20,
      totalAmount: 2500,
      orderstatus: "Prepareing"
    });
    this.orders.push({
      orderId: "231",
      mobile: "87898934525",
      customerName: "Jake",
      noOfItemsOrdered: 5,
      totalAmount: 700,
      orderstatus: "Ready to serve"
    });
    this.orders.push({
      orderId: "231",
      mobile: "87898934525",
      customerName: "Jake",
      noOfItemsOrdered: 5,
      totalAmount: 700,
      orderstatus: "Order Recived"
    });
    this.orders.push({
      orderId: "231",
      mobile: "87898934525",
      customerName: "Jake",
      noOfItemsOrdered: 5,
      totalAmount: 700,
      orderstatus: "Prepareing"
    });
    this.orders.push({
      orderId: "231",
      mobile: "87898934525",
      customerName: "Jake",
      noOfItemsOrdered: 5,
      totalAmount: 700,
      orderstatus: "Ready to serve"
    });
    this.orders.push({
      orderId: "231",
      mobile: "87898934525",
      customerName: "Jake",
      noOfItemsOrdered: 5,
      totalAmount: 700,
      orderstatus: "Prepareing"
    });
    this.orders.push({
      orderId: "231",
      mobile: "87898934525",
      customerName: "Jake",
      noOfItemsOrdered: 5,
      totalAmount: 700,
      orderstatus: "Ready to serve"
    });
    this.orders.push({
      orderId: "231",
      mobile: "87898934525",
      customerName: "Jake",
      noOfItemsOrdered: 5,
      totalAmount: 700,
      orderstatus: "Order Recived"
    });
    this.orders.push({
      orderId: "231",
      mobile: "87898934525",
      customerName: "Jake",
      noOfItemsOrdered: 5,
      totalAmount: 700,
      orderstatus: "Prepareing"
    });
    this.filteredOrders = [];
    this.filteredOrders = this.filteredOrders.concat(this.orders);
  },
  methods: {
    onStatusChange(status, orderId) {
      var orders = [...this.orders];
      for (let orderIndex = 0; orderIndex < orders.length; orderIndex++) {
        const order = orders[orderIndex];
        if (order.orderId == orderId) {
          orders[orderIndex].orderstatus = status;
          this.orders = orders;
          break;
        }
      }
    },
    getNewOrders() {
      this.filteredOrders = this.orders.filter(
        order => order.orderstatus == "Order Recived"
      );
    },
    getPreparingOrders() {
      this.filteredOrders = this.orders.filter(
        order => order.orderstatus == "Prepareing"
      );
    },
    getReadyOrders() {
      this.filteredOrders = this.orders.filter(
        order => order.orderstatus == "Ready to serve"
      );
    },
    showAll() {
      this.filteredOrders = [];
      this.filteredOrders = this.filteredOrders.concat(this.orders);
    }
  }
};
</script>

<style>
body {
  font-family: "Lato", sans-serif;
}
header {
  margin: -8px -8px 0 -8px;
  height: 60px;
  background-color: #111;
}
.logo{
  border-radius: 5px;
  background-color: gray;
  float: left;
  width: 80px;
  height: 50px;
}
.main {
  font-size: 28px; /* Increased text to enable scrolling */
  height: 100%;
}
/* Responsive header */
@media screen and (max-width: 600px) {
  
  header{
      margin: 0;
      width: 100vw;
  }
}
.tab {
  display: flex;
  justify-content: center;
  align-items: center;
}
.tab-button {
  background-color: rgba(255, 255, 255, 0);
  color: #818181;
  font-size: 20px;
  min-width: 90px;
  height: 60px;
  border: 0;
  padding: 10px;
  margin: 0 10px 0 10px;
}
.tab-button:hover {
  color: white;
}
/* Remove extra left and right margins, due to padding */
.row {
  margin: 0 -5px;
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}
/* Responsive header */
@media screen and (max-width: 600px) {
  .tab-button {
  background-color: rgba(255, 255, 255, 0);
  color: #818181;
  font-size: 15px;
  height: 60px;
  border: 0;
  padding: 10px;
  /* margin: 0 10px 0 10px; */
}
}
</style>
