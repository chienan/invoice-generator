<template>
  <div class="container" ref="container">
    <div class="invoice" id="invoice">
      <div class="nav">
        <div class="main-title">INVOICE GENERATOR</div>
        <div class="main-description">calculate & get invoice easily!</div>
      </div>

      <div class="invoice-title section">
        <div class="invoice-title-title title">INVOICE TITLE</div>
        <div class="invoice-title-form">
          <div class="form-section">
            <label class="sr-only" for="title">InvoiceTitle</label>

            <b-form-input
              id="title"
              v-model="invoice_title"
              ref="title"
              placeholder="InvoiceTitle"
              class="input-type1"
            ></b-form-input>
          </div>
        </div>
      </div>
      <!--invoice from-->
      <div class="client-name section">
        <div class="client-details-container">
          <div class="client-details-title">INVOICE from</div>
          <!-- <div class="client-details-edit">EDIT</div> -->
        </div>

        <div class="client-details-content">
          <div class="client-details-name">
            <input
              type="text"
              class="input-from-name input-type2"
              placeholder="HAYABUSA corp."
              v-model="from_name"
            />
            <span class="focus-border"></span>
          </div>
          <div class="client-details-address">
            <input
              type="text"
              class="input-from-address input-type3"
              placeholder="台北市內湖區公道路5號"
              v-model="from_address"
            />
            <span class="focus-border-2"></span>
          </div>

          <div class="client-details-phone">
            <input
              type="tel"
              class="input-from-phone input-type3"
              placeholder="+886 897832490"
              v-model="from_tel"
            />
            <span class="focus-border-2"></span>
          </div>
          <div class="client-details-email">
            <input
              type="email"
              class="input-from-email input-type3"
              placeholder="hayabusa@example.com"
              v-model="from_email"
            />
            <span class="focus-border-2"></span>
          </div>
        </div>
      </div>

      <!--invoice to-->
      <div class="client-details section">
        <div class="client-details-container">
          <div class="client-details-title">INVOICE to</div>
          <!-- <div class="client-details-edit">EDIT</div> -->
        </div>

        <div class="client-details-content">
          <div class="client-details-name">
            <input
              type="text"
              class="input-to-name input-type2"
              placeholder="Radius Lab"
              v-model="to_name"
            />
            <span class="focus-border"></span>
          </div>
          <div class="client-details-address">
            <input
              type="text"
              class="input-to-address input-type3"
              placeholder="新竹市大學路300號5樓"
              v-model="to_address"
            />
            <span class="focus-border-2"></span>
          </div>

          <div class="client-details-phone">
            <input
              type="tel"
              class="input-to-phone input-type3"
              placeholder="+886 847374958"
              v-model="to_tel"
            />
            <span class="focus-border-2"></span>
          </div>
          <div class="client-details-email">
            <input
              type="email"
              class="input-to-email input-type3"
              placeholder="Anenome@example.com"
              v-model="to_email"
            />
            <span class="focus-border-2"></span>
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

            <b-form-input
              class="input-type1"
              id="count"
              placeholder="0001"
              v-model="invoice_number"
            ></b-form-input>
            <span class="focus-border"></span>
          </div>
        </div>

        <!--  invoice-date  -->
        <div class="invoice-date">
          <div class="invoice-date-title title">INVOICE DATE</div>
          <div class="invoice-date-form">
            <div class="invoie-number-form">
              <label class="sr-only" for="date">invoiceDate</label>

              <b-form-input
                id="date"
                class="input-type1"
                placeholder="0001"
                type="date"
                v-model="invoice_date"
              ></b-form-input>
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
                <b-form-input
                  id="description"
                  class="input-type1"
                  placeholder="chocolate"
                  v-model="items.description"
                ></b-form-input>
              </td>

              <td class="item item-quantity">
                <b-form-input
                  id="quantity"
                  class="input-type1"
                  placeholder="3"
                  v-model="items.quantity"
                  v-on:change="itemTotal(index)"
                ></b-form-input>
              </td>

              <td class="item item-price">
                <b-form-input
                  id="price"
                  class="input-type1"
                  placeholder="200"
                  v-model="items.price"
                  v-on:change="itemTotal(index)"
                ></b-form-input>
              </td>

              <td class="item item-discount">
                <b-form-input
                  id="discount"
                  class="input-type1"
                  placeholder="5"
                  v-model="items.discount"
                  v-on:change="itemTotal(index)"
                ></b-form-input>
              </td>
              <td class="item item-tax">
                <b-form-input
                  id="tax"
                  class="input-type1"
                  placeholder="3"
                  v-model="items.tax"
                  v-on:change="itemTotal(index)"
                ></b-form-input>
              </td>
              <td class="item item-total">
                <b-form-input class="input-type1" placeholder="8" :value="items.total | money"></b-form-input>
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

        <textarea
          class="client-notes-textarea"
          name="client-notes"
          id="client-notes"
          cols="30"
          rows="10"
          placeholder="such as 'thank you for your business'"
          v-model="notes"
        ></textarea>
      </div>

      <div class="save-section section">
        <!-- scroll down UI -->
        <div v-if="scroll" class="scroll-section" ref="scroll">
          <div class="scroll-down">
            <div class="chevron"></div>
            <div class="chevron"></div>
            <div class="chevron"></div>
            <span class="text">Scroll down</span>
          </div>
        </div>
        <button class="btn-preview" @click.stop.prevent="previewInvoice">preview</button>
      </div>
    </div>

    <!--  preview invoice  -->

    <div v-if="preview" class="container-preview">
      <div class="preview-invoice-container" ref="content" id="preview-invoice">
        <div class="preview-title section">
          {{ invoice_title.length ? invoice_title : 'INVOICE' }}
          <!-- INVOICE TITLE: {{invoice_title}} -->
        </div>

        <div class="preview-invoice-contact section">
          <div class="preview-invoice-from">
            INVOICE form
            <div class="preview-from-name preview">{{from_name}}</div>
            <div class="preview-from-address preview">{{from_address}}</div>
            <div class="preview-from-tel preview">{{from_tel}}</div>
            <div class="preview-from-email preview">{{from_email}}</div>
          </div>

          <div class="preview-invoice-to">
            INVOICE to
            <div class="preview-to-name preview">{{to_name}}</div>
            <div class="preview-to-address preview">{{to_address}}</div>
            <div class="preview-to-tel preview">{{to_tel}}</div>
            <div class="preview-to-email preview">{{to_email}}</div>
          </div>
        </div>

        <div class="preview-invoice-detail section">
          <div class="preview-invoice-number">
            INVOICE NO:
            <div class="preview">{{invoice_number}}</div>
          </div>
          <div class="preview-invoice-date">
            INVOICE DATE:
            <div class="preview">{{invoice_date}}</div>
          </div>
        </div>

        <div class="product-section section">
          <div class="product-section-title">
            PRODUCT
            <div class="product-section-amount">({{indexLength ? indexLength : 0}})</div>
          </div>

          <table class="product-container">
            <thead>
              <tr class="items-section">
                <td class="item preview-item-description">DESCRIPTION</td>
                <td class="item preview-item-quantity">QTY.</td>
                <td class="item preview-item-price">PRICE</td>
                <td class="item preview-item-discount">DISC.%</td>
                <td class="item preview-item-tax">TAX%</td>
                <td class="item preview-item-total">TOTAL</td>
              </tr>
            </thead>
            <tbody>
              <tr
                class="items-section-preview preview"
                v-for="(items, index) in items"
                :key="index"
              >
                <td class="item preview-item-description">{{items.description}}</td>

                <td class="item preview-item-quantity">{{items.quantity}}</td>

                <td class="item preview-item-price">{{items.price}}</td>

                <td class="item preview-item-discount">{{items.discount}}</td>
                <td class="item preview-item-tax">{{items.tax}}</td>

                <td class="item preview-item-total">{{items.total}}</td>
              </tr>
            </tbody>
            <tfoot>
              <tr class="items-section final-section">
                <td class="final-preview-title">DISCOUNT</td>
                <td class="final-preview-number line">{{itemsDiscountTotal | money}}</td>
              </tr>
              <tr class="items-section final-section">
                <td class="final-preview-title">TAX</td>
                <td class="final-preview-number line">{{itemsTaxTotal | money}}</td>
              </tr>
              <tr class="items-section final-section">
                <td class="final-preview-title">TOTAL</td>
                <td class="final-preview-number">{{itemsTotal | money}}</td>
              </tr>
            </tfoot>
          </table>
        </div>
        <div v-if="notes.length > 0" class="client-notes section">
          <div class="client-notes-title">NOTES FOR CLIENT</div>
          <div class="client-notes-container">{{notes}}</div>
        </div>
      </div>
    </div>

    <!-- download pdf -->
    <div v-if="preview" class="save-section section">
      <button class="save-btn" @click.stop.prevent="generateReport()">
        <img src="https://i.imgur.com/vdESFr3.png" class="save-icon" alt />
      </button>
    </div>
  </div>
</template>

<script>
import { jsPDF } from "jspdf";
import * as html2canvas from "html2canvas";

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
      ],
      notes: "",
      preview: false,
      scroll: false
    };
  },
  created() {
    setTimeout(() => {
      this.$refs.title.focus();
    });
  },
  methods: {
    generateReport() {
      window.scrollTo(0, 0); //Before calling html2canvas, the window needs to be at the (0,0) to capture the entire DOM.

      var doc = new jsPDF("p", "mm", "a4");
      html2canvas(document.querySelector("#preview-invoice")).then(function(
        canvas
      ) {
        const imgData = canvas.toDataURL("image/png");
        // eslint-disable-next-line no-unused-vars
        const pageHeight = 500;
        const imgWidth = (canvas.width * 50) / 390;
        const imgHeight = (canvas.height * imgWidth) / canvas.width;
        // eslint-disable-next-line no-unused-vars
        const heightLeft = imgHeight;
        const top = 15;

        doc.addImage(imgData, "PNG", 15, top, imgWidth, imgHeight);

        doc.save(Date.now() + ".pdf");
      });
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
    },

    //preview invoice
    previewInvoice() {
      this.preview = true;
      this.scroll = true;
      setTimeout(() => (this.scroll = false), 3500);
    }
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
/* main contents */
.nav {
  /* display: flex;
  justify-content: flex-end;
  align-items: center; */
  color: #ffffff;
  position: relative;
  margin-top: 15px;
  padding-bottom: 15px;
  background-image: url(https://i.imgur.com/MZZZrtR.jpg);
  background-size: cover;
  background-position: center;
  height: 350px;
  border-radius: 8px;
}

.main-title {
  position: absolute;
  bottom: 45px;
  right: 15px;
  font-size: 2rem;
}

.main-description {
  position: absolute;
  bottom: 18px;
  right: 19px;
  font-size: 0.9rem;
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
  box-shadow: 2px 2px 50px 12px rgba(0, 0, 0, 0.1);
}

.nav,
.invoice-title,
.client-name,
.client-details,
.product-section,
.client-notes,
.preview-title,
.preview-invoice-contact,
.preview-invoice-detail {
  border-bottom: 1px solid #dcdcdc;
}

.client-name-form,
.invoice-info,
.client-details-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

.add-new-section,
.client-details-edit {
  display: flex;
  justify-content: center;
  align-items: center;
}

.form-section {
  display: flex;
  align-items: center;
}

.title {
  margin-bottom: 10px;
}

#title {
  width: 50%;
}

.form-section,
.client-details-title {
  width: 100%;
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
  /* border: 2px dashed #ecf5ff; */
  padding: 20px 25px;
  margin-top: 15px;
  color: #666666;
  font-size: 15px;
  font-weight: normal;
  background: #ecf5ff;
  border-radius: 5px;
}

.client-details-name {
  color: #000000;
  font-size: 18px;
  font-weight: 500;
  margin-bottom: 10px;
  position: relative;
}

.client-details-address,
.client-details-phone,
.client-details-email {
  position: relative;
}

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
  background: #4a4aff;
  height: 38px;
  width: 38px;
  bottom: 120px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 2px 2px 10px 3px rgba(0, 0, 0, 0.2);
}

.add-product:hover {
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
  position: relative;
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

/* scroll down UI */

.scroll-section {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  right: 320px;
  font-weight: 530;
  letter-spacing: 0.5px;
}

.scroll-down {
  display: flex;
  justify-content: center;
  position: relative;
  width: 24px;
  height: 24px;
}

.chevron {
  position: absolute;
  width: 28px;
  height: 8px;
  opacity: 0;
  transform: scale3d(0.5, 0.5, 0.5);
  animation: move 3s ease-out infinite;
}

.chevron:first-child {
  animation: move 3s ease-out 1s infinite;
}

.chevron:nth-child(2) {
  animation: move 3s ease-out 2s infinite;
}

.chevron:before,
.chevron:after {
  content: " ";
  position: absolute;
  top: 0;
  height: 100%;
  width: 51%;
  background: #4a4aff;
}

.chevron:before {
  left: 0;
  transform: skew(0deg, 30deg);
}

.chevron:after {
  right: 0;
  width: 50%;
  transform: skew(0deg, -30deg);
}

@keyframes move {
  25% {
    opacity: 1;
  }
  33% {
    opacity: 1;
    transform: translateY(30px);
  }
  67% {
    opacity: 1;
    transform: translateY(40px);
  }
  100% {
    opacity: 0;
    transform: translateY(55px) scale3d(0.5, 0.5, 0.5);
  }
}

.text {
  font-size: 12px;
  color: #4a4aff;
  text-transform: uppercase;
  white-space: nowrap;
  opacity: 0.25;
  animation: pulse 2s linear alternate infinite;
}

@keyframes pulse {
  to {
    opacity: 1;
  }
}

/* preview-section */
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

.preview-title {
  font-size: 22px;
  color: #bebebe;
}

.preview {
  font-size: 15px;
  font-weight: 500;
  color: #5b5b5b;
}

.preview-invoice-contact {
  display: flex;
}

.preview-invoice-from,
.preview-invoice-to {
  width: 50%;
}

.preview-from-name,
.preview-to-name {
  font-size: 18px;
  margin: 7px 0px;
}

.preview-invoice-number {
  margin-bottom: 15px;
}

.items-section-preview {
  display: flex;
  margin: 5px 0px;
}

.preview-item-description {
  width: 35%;
}

.preview-item-quantity {
  width: 10%;
}

.preview-item-price {
  width: 15%;
}

.preview-item-discount {
  width: 15%;
}

.preview-item-tax {
  width: 13%;
}

.preview-item-total {
  width: 17%;
}

.final-preview-title {
  width: 83%;
  text-align: end;
  margin-right: 15px;
  /* margin-right: 15%; */
  color: rgba(0, 0, 0, 0.2);
}

.final-preview-number {
  position: relative;
  width: 17%;
}

.final-preview-total {
  color: #ffffff;
}

/* .client-notes-container {
  height: 80%;
} */
</style>