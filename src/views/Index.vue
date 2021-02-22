<template>
  <div class="container">
    <div class="nav">
      <h3>invoice generator</h3>
    </div>
    <div class="invoice-title">Invoice 2021</div>
    <div class="client-name">
      <div class="client-name-title">INVOICE TO</div>
      <div class="client-name-form"></div>
    </div>
    <div class="client-details">CLIENT DETAILS</div>
  </div>
</template>


<style scoped>
@media screen and (max-width: 480px) {
  .container {
    height: 100%;
    width: 100%;
    border: 1px solid gray;
  }
  .nav {
    border: 1px solid gray;
  }
  .invoice-title {
    border: 1px solid gray;
  }
  .client-name {
    border: 1px solid gray;
  }
  .client-details {
    border: 1px solid gray;
  }
}
</style>