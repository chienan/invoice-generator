<template>
  <form class="container" id="invoice" ref="content" @submit.stop.prevent="download">
    <div class="nav">
      <img src="https://i.imgur.com/FbsYH3N.png" class="main-logo" alt />
      <div class="main-title">TOSO INVOICE GENERATOR</div>
    </div>

    <div class="invoice-title section">
      <div class="invoice-title-title title">INVOICE TITLE</div>
      <div class="invoice-title-form">
        <div class="form-section">
          <label class="sr-only" for="title">InvoiceTitle</label>

          <b-form-input id="title" placeholder="InvoiceTitle"></b-form-input>
        </div>
      </div>
    </div>
    <!--invoice from-->
    <div class="client-name section">
      <div class="client-details-container">
        <div class="client-details-title">INVOICE from</div>
        <div class="client-details-edit">EDIT</div>
      </div>

      <div class="client-details-content">
        <div class="client-details-name">
          <input type="text" class="input-from-name" placeholder="HAYABUSA corp." />
        </div>
        <div class="client-details-address">
          <input type="text" class="input-from-address" placeholder="台北市內湖區公道路5號" />
        </div>

        <div class="client-details-phone">
          <input type="tel" class="input-from-phone" placeholder="+886 897832490" />
        </div>
        <div class="client-details-email">
          <input type="email" class="input-from-email" placeholder="hayabusa@example.com" />
        </div>
      </div>
    </div>
    <!-- <div class="client-name section">
      <div class="client-name-title title">INVOICE TO</div>
      <div class="client-name-form">
        <div class="form-section">
          <label class="sr-only" for="name">ClientName</label>
          <b-input-group prepend="@" class="mb-2 mr-sm-2 mb-sm-0">
            <b-form-input id="name" placeholder="ClientName"></b-form-input>
          </b-input-group>
        </div>
        <div class="add-new-section">＋ NEW</div>
      </div>
    </div>-->

    <!--invoice to-->
    <div class="client-details section">
      <div class="client-details-container">
        <div class="client-details-title">INVOICE to</div>
        <div class="client-details-edit">EDIT</div>
      </div>

      <div class="client-details-content">
        <div class="client-details-name">
          <input type="text" class="input-to-name" placeholder="Radius Lab" />
        </div>
        <div class="client-details-address">
          <input type="text" class="input-to-address" placeholder="新竹市大學路300號5樓" />
        </div>

        <div class="client-details-phone">
          <input type="tel" class="input-to-phone" placeholder="+886 847374958" />
        </div>
        <div class="client-details-email">
          <input type="email" class="input-to-email" placeholder="Anenome@example.com" />
        </div>
      </div>
    </div>

    <!-- invoice-info -->
    <div class="invoice-info section">
      <!-- invoice-number -->
      <div class="invoice-number">
        <div class="invoice-number-title title">INVOICE NO.</div>
        <div class="invoie-number-form">
          <label class="sr-only" for="count">invoiceNo</label>

          <b-form-input id="count" placeholder="0001"></b-form-input>
        </div>
      </div>

      <!--  invoice-date  -->
      <div class="invoice-date">
        <div class="invoice-date-title title">INVOICE DATE</div>
        <div class="invoice-date-form">
          <div class="invoie-number-form">
            <label class="sr-only" for="date">invoiceDate</label>

            <b-form-input id="date" placeholder="0001" type="date"></b-form-input>
          </div>
        </div>
      </div>
    </div>

    <!--  product section  -->
    <div class="product-section section">
      <div class="product-section-title">
        PRODUCT
        <div class="product-section-amount">(0)</div>
      </div>

      <button class="add-product" @click.stop.prevent="addItem(index)">
        <div class="btn-add-product">＋</div>
      </button>
      <table class="product-container">
        <thead>
          <tr class="items-section">
            <td class="item item-description">DESCRIPTION</td>
            <td class="item item-quantity">QUANTITY</td>
            <td class="item item-price">PRICE</td>
            <td class="item item-discount">DISCOUNT</td>
            <td class="item item-tax">TAX</td>
            <td class="item item-remove"></td>
          </tr>
        </thead>
        <tbody>
          <tr class="items-section" v-for="(items, index) in items" :key="index">
            <td class="item item-description">
              <label class="sr-only" for="description">itemDescription</label>
              <b-form-input id="description" placeholder="chocolate" v-model="items.description"></b-form-input>
            </td>

            <td class="item item-quantity">
              <label class="sr-only" for="quantity">itemQuantity</label>
              <b-form-input id="quantity" placeholder="3psc" v-model="items.quantity"></b-form-input>
            </td>

            <td class="item item-price">
              <label class="sr-only" for="price">itemPrice</label>
              <b-form-input id="price" placeholder="$200" v-model="items.price"></b-form-input>
            </td>

            <td class="item item-discount">
              <label class="sr-only" for="discount">itemDiscount</label>
              <b-form-input id="discount" placeholder="-15" v-model="items.discount"></b-form-input>
            </td>
            <td class="item item-tax">
              <label class="sr-only" for="tax">itemTax</label>
              <b-form-input id="tax" placeholder="$8" v-model="items.tax"></b-form-input>
            </td>
            <td class="item item-remove">
              <button class="btn-item-remove" @click.stop.prevent="removeItem(index)">×</button>
            </td>
          </tr>
          <tr class="item-total">
            <th>$594</th>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- client notes -->
    <div class="client-notes section">
      <div class="client-notes-title">CLIENT-NOTES</div>
      <div class="client-notes-show">
        <div class="client-notes-icon"></div>
      </div>
    </div>

    <div class="save-section">
      <button class="save-btn" type="submit">
        <img src="https://i.imgur.com/vdESFr3.png" class="save-icon" alt />
      </button>
    </div>
  </form>
</template>

<script>
// import jspdf from "jspdf";
import * as html2pdf from "html2pdf.js";

export default {
  data() {
    return {
      items: [
        {
          description: "",
          quantity: "",
          price: "",
          discount: "",
          tax: ""
        }
      ]
    };
  },
  methods: {
    download() {
      const element = document.querySelector("#invoice");
      const opt = {
        margin: 3,
        filename: "invoice.pdf",
        image: { type: "jpeg", quality: 1 },
        html2canvas: { scale: 2 }
      };

      html2pdf()
        .from(element)
        .set(opt)
        .save();
    },

    addItem(index) {
      this.items.splice(index + 1, 0, {
        description: "",
        quantity: "",
        price: "",
        discount: "",
        tax: ""
      });
    },

    removeItem(index) {
      this.items.splice(index, 1);
    }

    // download(e) {
    //   const doc = new jspdf();
    //   const contentHtml = this.$refs.content.innerHTML;

    //   const form = e.target;
    //   const formData = new FormData(form);

    //   console.log(formData);

    //   doc.html(contentHtml, {
    //     x: 15,
    //     y: 15,
    //     width: 200
    //   });

    //   doc.save("output.pdf");
    // }
  }
};
</script>


<style>
.nav {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  margin-top: 15px;
  padding-bottom: 15px;
}

.main-logo {
  width: 8%;
  margin-right: 10px;
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

.container {
  height: 100%;
  width: 100%;
  border: 1px solid #dcdcdc;
  max-width: 720px;
}

.nav,
.invoice-title,
.client-name,
.client-details,
.product-section,
.client-notes {
  border-bottom: 1px solid #dcdcdc;
}

.client-name-form,
.invoice-info,
.client-details-container {
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

.title {
  margin-bottom: 10px;
}

.form-section,
.client-details-title {
  width: 80%;
}

.input-to-name,
.input-to-address,
.input-to-phone,
.input-to-email,
.input-from-name,
.input-from-address,
.input-from-phone,
.input-from-email {
  border: none;
  width: 75%;
}

.add-new-section,
.client-details-edit {
  font-size: 5px;
  font-weight: 550;
  color: #4a4aff;
  width: 20%;
}

.client-details-content {
  border: 2px dashed #dcdcdc;
  padding: 20px 25px;
  margin-top: 15px;
  color: #666666;
  font-size: 15px;
  font-weight: normal;
}

.client-details-name {
  color: #000000;
  font-size: 18px;
  font-weight: 500;
  margin-bottom: 10px;
}
/* 
.client-details-1,
.client-details-2 {
  color: #666666;
  font-size: 15px;
  font-weight: normal;
} */

.invoice-number {
  width: 47%;
}

.invoice-date {
  width: 47%;
}

.product-section {
  display: flex;
  flex-direction: column;
  position: relative;
}

.product-section-title {
  display: flex;
}

.items-section {
  display: flex;
}

.item-description {
  width: 35%;
}

.item-quantity {
  width: 15%;
}

.item-price {
  width: 20%;
}

.item-discount {
  width: 15%;
}

.item-tax {
  width: 15%;
}

.item-remove {
  width: 5%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn-item-remove {
  font-size: 25px;
  font-weight: 300;
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
</style>