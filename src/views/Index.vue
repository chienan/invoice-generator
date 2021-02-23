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
        <div class="add-new-section">＋ NEW</div>
      </div>
    </div>
    <div class="client-details section">
      <div class="client-details-title">CLIENT DETAILS</div>
      <div class="client-details-edit">EDIT</div>
    </div>
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

            <b-form-input id="inline-form-input-invoiceDate" placeholder="0001" type="date"></b-form-input>
          </div>
        </div>
      </div>
    </div>

    <div class="product-section section">
      <div class="product-section-title">PRODUCT</div>
      <div class="product-section-amount">(0)</div>
      <div class="add-product">
        <div class="btn-add-product">＋</div>
      </div>
    </div>
    <div class="client-notes section">
      <div class="client-notes-title">CLIENT-NOTES</div>
      <div class="client-notes-show">
        <div class="client-notes-icon"></div>
      </div>
    </div>

    <div class="save-section">
      <div class="save-btn">
        <img src="https://i.imgur.com/vdESFr3.png" class="save-icon" alt />
      </div>
    </div>
  </div>
</template>


<style>
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
    border-bottom: 1px solid #9d9d9d;
  }

  .section {
    margin-top: 20px;
    /* margin-bottom: 20px; */
    padding-bottom: 20px;
    color: #9d9d9d;
    font-size: 13px;
    font-weight: 530;
    letter-spacing: 0.5px;
  }

  .client-name-form,
  .invoice-info,
  .client-details {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .form-section,
  .add-new-section,
  .client-details-edit {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .form-section,
  .client-details-title {
    width: 80%;
  }
  .add-new-section,
  .client-details-edit {
    font-size: 5px;
    font-weight: 550;
    color: #4a4aff;
    width: 20%;
  }

  .invoice-number {
    width: 47%;
  }

  .invoice-date {
    width: 47%;
  }

  .product-section {
    display: flex;
    position: relative;
  }

  .product-section-amount {
    color: #bebebe;
  }

  .add-product {
    position: absolute;
    border: 1px solid #4a4aff;
    background: #4a4aff;
    height: 38px;
    width: 38px;
    right: 15px;
    bottom: 13px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 2px 2px 10px 3px rgba(0, 0, 0, 0.2);
  }

  .btn-add-product {
    color: #ffffff;
    border: 1px solid #ffffff;
    border-radius: 50%;
    height: 16px;
    width: 16px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .client-notes {
    position: relative;
  }

  .client-notes-show {
    position: absolute;
    border: 2px solid #4a4aff;
    color: #4a4aff;
    border-radius: 50%;
    height: 16px;
    width: 16px;
    display: flex;
    justify-content: center;
    align-items: center;
    right: 26px;
    bottom: 20px;
  }

  .client-notes-icon {
    width: 0;
    height: 0;
    border-style: solid;
    border-width: 5px 4px 0 4px;
    border-color: #4a4aff transparent transparent transparent;
  }

  .save-section {
    display: flex;
    flex-direction: row-reverse;
  }

  .save-btn {
    border: 1px solid #4a4aff;
    background: #4a4aff;
    height: 38px;
    width: 38px;
    /* right: 15px;
    bottom: 13px; */
    margin: 15px 15px 15px 0;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 2px 2px 10px 3px rgba(0, 0, 0, 0.2);
  }

  .save-icon {
    width: 35%;
  }
}
</style>