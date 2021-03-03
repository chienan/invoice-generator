<template>
  <div class="container">
    <form class="invoice" id="invoice" ref="content" @submit.stop.prevent="download">
      <div class="nav">
        <img src="https://i.imgur.com/FbsYH3N.png" class="main-logo" alt />
        <div class="main-title">TOSO INVOICE GENERATOR</div>
      </div>

      <div class="invoice-title section">
        <div class="invoice-title-title title">INVOICE TITLE</div>
        <div class="invoice-title-form">
          <div class="form-section">
            <label class="sr-only" for="title">InvoiceTitle</label>

            <b-form-input id="title" v-model="invoice_title" placeholder="InvoiceTitle"></b-form-input>
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
            <input
              type="text"
              class="input-from-name"
              placeholder="HAYABUSA corp."
              v-model="from_name"
            />
          </div>
          <div class="client-details-address">
            <input
              type="text"
              class="input-from-address"
              placeholder="台北市內湖區公道路5號"
              v-model="from_address"
            />
          </div>

          <div class="client-details-phone">
            <input
              type="tel"
              class="input-from-phone"
              placeholder="+886 897832490"
              v-model="from_tel"
            />
          </div>
          <div class="client-details-email">
            <input
              type="email"
              class="input-from-email"
              placeholder="hayabusa@example.com"
              v-model="from_email"
            />
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
            <input type="text" class="input-to-name" placeholder="Radius Lab" v-model="to_name" />
          </div>
          <div class="client-details-address">
            <input
              type="text"
              class="input-to-address"
              placeholder="新竹市大學路300號5樓"
              v-model="to_address"
            />
          </div>

          <div class="client-details-phone">
            <input type="tel" class="input-to-phone" placeholder="+886 847374958" v-model="to_tel" />
          </div>
          <div class="client-details-email">
            <input
              type="email"
              class="input-to-email"
              placeholder="Anenome@example.com"
              v-model="to_email"
            />
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

            <b-form-input id="count" placeholder="0001" v-model="invoice_number"></b-form-input>
          </div>
        </div>

        <!--  invoice-date  -->
        <div class="invoice-date">
          <div class="invoice-date-title title">INVOICE DATE</div>
          <div class="invoice-date-form">
            <div class="invoie-number-form">
              <label class="sr-only" for="date">invoiceDate</label>

              <b-form-input id="date" placeholder="0001" type="date" v-model="invoice_date"></b-form-input>
            </div>
          </div>
        </div>
      </div>

      <!--  product section  -->
      <div class="product-section section">
        <div class="product-section-title">
          PRODUCT
          <div class="product-section-amount">({{indexLength ? indexLength : 0}})</div>
        </div>

        <button class="add-product" @click.stop.prevent="addItem(index)">
          <div class="btn-add-product">＋</div>
        </button>

        <div class="add-product-notice">Add line</div>
        <table class="product-container">
          <thead>
            <tr class="items-section">
              <td class="item item-description">DESCRIPTION</td>
              <td class="item item-quantity">QTY.</td>
              <td class="item item-price">PRICE</td>
              <td class="item item-discount">DISC.%</td>
              <td class="item item-tax">TAX%</td>
              <td class="item item-total">TOTAL</td>
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
                <b-form-input
                  id="quantity"
                  placeholder="3"
                  v-model="items.quantity"
                  v-on:change="itemTotal(index)"
                ></b-form-input>
              </td>

              <td class="item item-price">
                <label class="sr-only" for="price">itemPrice</label>
                <b-form-input
                  id="price"
                  placeholder="200"
                  v-model="items.price"
                  v-on:change="itemTotal(index)"
                ></b-form-input>
              </td>

              <td class="item item-discount">
                <label class="sr-only" for="discount">itemDiscount</label>
                <b-form-input
                  id="discount"
                  placeholder="5"
                  v-model="items.discount"
                  v-on:change="itemTotal(index)"
                ></b-form-input>
              </td>
              <td class="item item-tax">
                <label class="sr-only" for="tax">itemTax</label>
                <b-form-input
                  id="tax"
                  placeholder="3"
                  v-model="items.tax"
                  v-on:change="itemTotal(index)"
                ></b-form-input>
              </td>
              <td class="item item-total">
                <label class="sr-only" for="tax">itemTotal</label>
                <b-form-input id="tax" placeholder="8" :value="items.total | money"></b-form-input>
              </td>
              <td class="item item-remove">
                <button class="btn-item-remove" @click.stop.prevent="removeItem(index)">×</button>
              </td>
            </tr>
          </tbody>
          <tfoot>
            <tr class="items-section final-section">
              <td class="final-title">DISCOUNT</td>
              <td class="final-number line">{{itemsDiscountTotal | money}}</td>
            </tr>
            <tr class="items-section final-section">
              <td class="final-title">TAX</td>
              <td class="final-number">{{itemsTaxTotal | money}}</td>
            </tr>
            <tr class="items-section final-section">
              <td class="final-title final-total">TOTAL</td>
              <td class="final-number total-container">{{itemsTotal | money}}</td>
            </tr>
          </tfoot>
        </table>
      </div>

      <!-- client notes -->
      <div class="client-notes section">
        <div class="client-notes-title">NOTES FOR CLIENT</div>
        <!-- <div class="client-notes-show">
        <button class="client-notes-icon"></button>
        </div>-->
        <textarea
          class="client-notes-textarea"
          name="client-notes"
          id="client-notes"
          cols="30"
          rows="10"
          placeholder="such as 'thank you for your business'"
        ></textarea>
      </div>

      <div class="save-section section">
        <button class="btn-preview">preview</button>
        <button class="save-btn" type="submit">
          <img src="https://i.imgur.com/vdESFr3.png" class="save-icon" alt />
        </button>
      </div>
    </form>

    <!--  preview invoice  -->

    <div class="container-preview">
      <div class="preview-title section">Invoice: {{invoice_title}}</div>

      <div class="preview-invoice-contact section">
        <div class="preview-invoice-from">
          Invoice form
          <div class="preview-from-name">{{from_name}}</div>
          <div class="preview-from-address">{{from_address}}</div>
          <div class="preview-from-tel">{{from_tel}}</div>
          <div class="preview-from-email">{{from_email}}</div>
        </div>

        <div class="preview-invoice-to">
          Invoice to
          <div class="preview-to-name">{{to_name}}</div>
          <div class="preview-to-address">{{to_address}}</div>
          <div class="preview-to-tel">{{to_tel}}</div>
          <div class="preview-to-email">{{to_email}}</div>
        </div>
      </div>

      <div class="preview-invoice-detail section">
        <div class="preview-invoice-number">Invoice number: {{invoice_number}}</div>
        <div class="preview-invoice-date">Invoice date: {{invoice_date}}</div>
      </div>

      <div class="product-section section">
        <div class="product-section-title">
          PRODUCT
          <div class="product-section-amount">({{indexLength ? indexLength : 0}})</div>
        </div>

        <table class="product-container">
          <thead>
            <tr class="items-section">
              <td class="item item-description">DESCRIPTION</td>
              <td class="item item-quantity">QTY.</td>
              <td class="item item-price">PRICE</td>
              <td class="item item-discount">DISC.%</td>
              <td class="item item-tax">TAX%</td>
              <td class="item item-total">TOTAL</td>
              <td class="item item-remove"></td>
            </tr>
          </thead>
          <tbody>
            <tr class="items-section" v-for="(items, index) in items" :key="index">
              <td class="item item-description">{{items.description}}</td>

              <td class="item item-quantity">{{items.quantity}}</td>

              <td class="item item-price">{{items.price}}</td>

              <td class="item item-discount">{{items.discount}}</td>
              <td class="item item-tax">{{items.tax}}</td>

              <td class="item item-total">{{items.total}}</td>
              <td class="item item-remove">
                <!-- <button class="btn-item-remove" @click.stop.prevent="removeItem(index)">×</button> -->
              </td>
            </tr>
          </tbody>
          <tfoot>
            <tr class="items-section final-section">
              <td class="final-title">DISCOUNT</td>
              <td class="final-number line">{{itemsDiscountTotal | money}}</td>
            </tr>
            <tr class="items-section final-section">
              <td class="final-title">TAX</td>
              <td class="final-number">{{itemsTaxTotal | money}}</td>
            </tr>
            <tr class="items-section final-section">
              <td class="final-title final-total">TOTAL</td>
              <td class="final-number total-container">{{itemsTotal | money}}</td>
            </tr>
          </tfoot>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
// import jspdf from "jspdf";
import * as html2pdf from "html2pdf.js";

export default {
  data() {
    return {
      invoice_title: "",
      from_name: "",
      from_address: "",
      from_tel: "",
      from_email: "",
      to_name: "",
      to_address: "",
      to_tel: "",
      to_email: "",
      index: 1,
      invoice_number: "",
      invoice_date: "",
      items: [
        {
          description: "",
          quantity: "",
          price: "",
          discount: "",
          discount_amount: "",
          tax: "",
          tax_amount: "",
          total: ""
        }
      ]
    };
  },
  methods: {
    // downlad invoice as pdf
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

    // add product
    addItem() {
      this.items.push({
        description: "",
        quantity: "",
        price: "",
        discount: "",
        discount_amount: "",
        tax: "",
        tax_amount: "",
        total: ""
      });
      this.index += 1;
    },

    //remove product
    removeItem(index) {
      this.items.splice(index, 1);
      this.index -= 1;
    },

    //calculate total
    itemTotal(index) {
      let discountTotal;
      let taxTotal;
      let taxDisTotal;

      //basic items total
      const calculatedTotal =
        this.items[index].quantity * this.items[index].price;
      this.items[index].total = calculatedTotal;

      // if discount applied
      if (this.items[index].discount) {
        discountTotal = calculatedTotal * (this.items[index].discount / 100);
        this.items[index].discount_amount = discountTotal;
        this.items[index].total = calculatedTotal - discountTotal;
      } else if (
        this.items[index].discount === 0 ||
        this.items[index].discount === ""
      ) {
        this.items[index].discount_amount = 0;
      }

      //if tax applied
      if (this.items[index].tax) {
        taxTotal = calculatedTotal * (this.items[index].tax / 100);
        this.items[index].tax_amount = taxTotal;
        this.items[index].total = calculatedTotal + taxTotal;
      } else if (this.items[index].tax === 0 || this.items[index].tax === "") {
        this.items[index].tax_amount = 0;
      }

      //if tax & discount applied

      if (this.items[index].tax && this.items[index].discount) {
        taxDisTotal =
          (calculatedTotal - discountTotal) * (this.items[index].tax / 100);
        this.items[index].discount_amount = discountTotal;
        this.items[index].tax_amount = taxDisTotal;
        this.items[index].total = calculatedTotal - discountTotal + taxDisTotal;
      }
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
  },
  computed: {
    indexLength() {
      return this.index;
    },
    //update final total
    itemsTotal() {
      return this.items.reduce((acc, item) => acc + item.total, 0);
    },
    itemsDiscountTotal() {
      return this.items.reduce((acc, item) => acc + item.discount_amount, 0);
    },
    itemsTaxTotal() {
      return this.items.reduce((acc, item) => acc + item.tax_amount, 0);
    }
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

.client-notes-title {
  margin-bottom: 10px;
}

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
  /* padding-bottom: 50px; */
}

.product-section-title {
  display: flex;
  margin-bottom: 10px;
}

.product-section-amount {
  margin-left: 5px;
}

.items-section {
  display: flex;
}

.final-section {
  min-height: 50px;
  align-items: center;
}

.item-description {
  width: 35%;
}

.item-quantity {
  width: 10%;
}

.item-price {
  width: 15%;
}

.item-discount {
  width: 10%;
}

.item-tax {
  width: 10%;
}

.item-total {
  width: 20%;
}

.item-remove {
  width: 5%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.final-title {
  width: 75%;
  text-align: end;
  margin-right: 15px;
  /* margin-right: 15%; */
  color: rgba(0, 0, 0, 0.2);
}

.final-number {
  position: relative;
  width: 25%;
}

.final-total {
  color: #ffffff;
}

.line::after {
  position: absolute;
  content: "";
  background-color: #dcdcdc;
  height: 1px;
  width: 190%;
  right: 25%;
  top: 165%;
}

.total-container::after {
  position: absolute;
  content: "";
  background-color: #4a4aff;
  border-radius: 5px;
  height: 200%;
  width: 190%;
  right: 25%;
  bottom: -50%;
  z-index: -1;
}

.total-container:hover::after {
  background-color: #9bd2ed;
}

/* .total-container::after::hover {
  position: absolute;
  content: "";
  background-color: black;
  border-radius: 5px;
  height: 200%;
  width: 190%;
  right: 25%;
  bottom: -50%;
  z-index: -1;
} */

.btn-item-remove {
  font-size: 25px;
  font-weight: 300;
}

.btn-item-remove:hover {
  color: #4a4aff;
}

.product-section-amount {
  color: #bebebe;
}

.add-product {
  position: absolute;
  /* border: 1px solid #4a4aff; */
  background: #4a4aff;
  height: 38px;
  width: 38px;
  /* right: 15px; */
  bottom: 120px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 2px 2px 10px 3px rgba(0, 0, 0, 0.2);
}

.add-product:hover {
  /* background: #88c8e7; */
  background: #9bd2ed;
}

.add-product-notice {
  position: absolute;
  bottom: 130px;
  left: 50px;
  font-weight: normal;
  color: #6a6a6a;
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
  /* position: absolute; */
  border: 2px solid #4a4aff;
  color: #4a4aff;
  border-radius: 50%;
  height: 16px;
  width: 16px;
  display: flex;
  justify-content: center;
  align-items: center;
  right: 26px;
  top: 0px;
  /* bottom: 20px; */
}
/* 
.client-notes-icon {
  width: 0;
  height: 0;
  border-style: solid;
  border-width: 5px 4px 0 4px;
  border-color: #4a4aff transparent transparent transparent;
} */

.client-notes-textarea {
  width: 100%;
  height: 10%;
  max-height: 100px;
  /* min-height: 20px; */
  border: 1px solid #dcdcdc;
  padding: 3%;
}

.save-section {
  display: flex;
  flex-direction: row-reverse;
}

.btn-preview {
  background: #4a4aff;
  height: 38px;
  width: 80px;
  color: #ffffff;
  border-radius: 5px;
  margin: 15px 15px 15px 0;
  box-shadow: 2px 2px 10px 3px rgba(0, 0, 0, 0.2);
}

.btn-preview:hover {
  background: #9bd2ed;
}

.save-btn {
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

.save-btn:hover {
  background: #9bd2ed;
}

.save-icon {
  width: 35%;
}

.preview-invoice-contact {
  display: flex;
}

.preview-invoice-from,
.preview-invoice-to {
  width: 50%;
}
</style>