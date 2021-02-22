<template>
  <div class="container">
    <div class="nav">
      <h3>invoice generator</h3>
    </div>
    <div class="invoice-title section">Invoice 2021</div>
    <div class="client-name section">
      <div class="client-name-title">INVOICE TO</div>
      <div class="client-name-form">
        <div class="form-section">
          <label class="sr-only" for="inline-form-input-username">ClientName</label>
          <b-input-group prepend="@" class="mb-2 mr-sm-2 mb-sm-0">
            <b-form-input id="inline-form-input-username" placeholder="ClientName"></b-form-input>
          </b-input-group>
        </div>
        <div class="add-new-section">new</div>
      </div>
    </div>
    <div class="client-details section">CLIENT DETAILS</div>
    <div class="invoice-info section">
      <div class="invoice-number">
        <div class="invoice-number-title">INVOICE NO.</div>
        <div class="invoie-number-form">
          <label class="sr-only" for="inline-form-input-invoiceNo">invoiceNo</label>

          <b-form-input id="inline-form-input-invoiceNo" placeholder="0001"></b-form-input>
        </div>
      </div>

      <div class="invoice-date">
        <div class="invoice-date-title">INVOICE DATE</div>
        <div class="invoice-date-form">
          <div class="invoie-number-form">
            <label class="sr-only" for="inline-form-input-invoiceDate">invoiceDate</label>

            <b-form-input id="inline-form-input-invoiceDate" placeholder="0001"></b-form-input>
          </div>
        </div>
      </div>
    </div>

    <div class="product-section section">PRODUCT(0)</div>
    <div class="client-notes section">CLIENT-NOTES</div>

    <div class="save-section">
      <div class="save-btn">save</div>
    </div>
  </div>
</template>


<style scoped>
@media screen and (max-width: 480px) {
  .container {
    height: 100%;
    width: 100%;
    border: 1px solid gray;
  }
  .nav,
  .invoice-title,
  .client-name,
  .client-details,
  .product-section,
  .client-notes {
    border-bottom: 1px solid gray;
  }

  .section {
    margin-top: 20px;
    /* margin-bottom: 20px; */
    padding-bottom: 20px;
  }

  .client-name-form,
  .invoice-info {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
  .form-section {
    width: 80%;
  }
  .add-new-section {
    width: 20%;
  }

  .invoice-number {
    width: 47%;
  }

  .invoice-date {
    width: 47%;
  }

  .save-section {
    display: flex;
    flex-direction: row-reverse;
  }
}
</style>