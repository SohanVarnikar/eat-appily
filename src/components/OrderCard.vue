<template>
  <div class="column">
    <div class="card">
      <h3 class="align-left">
        {{ order.customerName }}
        <p class="align-left contact">{{ order.mobile }}</p>
      </h3>
      <!-- <p class="align-left contact">{{ order.mobile }}</p> -->
      <p>
        <strong>No of Items :</strong>
        {{ order.noOfItemsOrdered }}
      </p>
      <p>
        <strong>Order Total :</strong>
        {{ order.totalAmount }}
      </p>
      <div :class="order.orderstatus | chipClass">{{ order.orderstatus }}</div>
      <button
        :disabled='order.orderstatus =="Ready to serve"'
        class="change-status-btn"
        @click="changeStatus(order)"
      >
        <strong>Change Status</strong>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "OrderCard",
  props: ["order", "onStatusChange"],
  filters: {
    chipClass(status) {
      if (status) {
        if (status == "Order Recived") {
          return "chip chip-orange";
        } else if (status == "Prepareing") {
          return "chip chip-red";
        } else {
          return "chip chip-green";
        }
      }
    }
  },
  methods: {
    changeStatus(order) {
      var status = "";
      if (order && order.orderstatus != "Ready to serve") {
        if (order.orderstatus == "Order Recived") {
          status = "Prepareing";
        } else if (order.orderstatus == "Prepareing") {
          status = "Ready to serve";
        }
      }
      this.$emit("onStatusChange", status, order.orderId);
    }
  }
};
</script>

<style>
/* Float four columns side by side */
.column {
  float: left;
  width: 33.33%;
  padding: 10px 10px;
}

/* Style the counter cards */
.card {
  font-size: 20px;
  padding: 16px;
  text-align: center;
  background-color: #f1f1f1;
}

.card:hover {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}
.align-left {
  text-align: left;
}
.contact {
  font-size: 12px;
}
.change-status-btn {
  background-color: rgb(59, 59, 59);
  color: white;
  font-size: 15px;
  border: 0;
  border-radius: 5px;
  padding: 5px;
  margin: 5px;
}
.change-status-btn:hover {
  background-color: rgb(112, 112, 112);
  color: rgb(8, 8, 8);
}
.change-status-btn[disabled] {
  pointer-events: none;
  opacity: 0.5;
}
.chip {
  border-radius: 5px;
  height: 40px;
  padding: 5px;
  text-align: center;
  text-transform: uppercase;
}
.chip-red {
  background-color: Red;
  color: white;
}
.chip-orange {
  background-color: orange;
  color: black;
}
.chip-green {
  background-color: rgb(80, 196, 80);
  color: black;
}
/* Responsive columns */
@media screen and (max-width: 600px) {
  .column {
    width: 100%;
    display: block;
    margin-bottom: 20px;
  }
}
</style>
