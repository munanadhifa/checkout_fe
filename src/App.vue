<template>
  <div class="app">
    <div class="container__step bg-[#FFFAE6]">
      <div v-for="(step, index) in steps" :key="index">
        <a v-if="currentStep >= step" class="group flex w-full items-center">
          <h3
            class="
              flex
              h-10
              w-10
              flex-shrink-0
              items-center
              justify-center
              rounded-full
              text-white
              bg-[#FF8A00]
              mt-1
            "
          >
            {{ step }}
          </h3>
          <h4 v-if="step === 1" class="ml-4 text-[#FF8A00]">Delivery</h4>
          <div v-if="step === 1">
            <svg
              class="w-2 text-[#FF8A00] ml-8"
              viewBox="0 0 22 80"
              fill="none"
              preserveAspectRatio="none"
            >
              <path
                d="M0 -2L20 40L0 82"
                vector-effect="non-scaling-stroke"
                stroke="currentcolor"
                stroke-linejoin="round"
              />
            </svg>
          </div>
          <h4 v-if="step === 2" class="ml-4 text-[#FF8A00]">Payment</h4>
          <div v-if="step === 2">
            <svg
              class="w-2 text-[#FF8A00] ml-8"
              viewBox="0 0 22 80"
              fill="none"
              preserveAspectRatio="none"
            >
              <path
                d="M0 -2L20 40L0 82"
                vector-effect="non-scaling-stroke"
                stroke="currentcolor"
                stroke-linejoin="round"
              />
            </svg>
          </div>
          <h4 v-if="step === 3" class="ml-4 text-[#FF8A00]">Finish</h4>
        </a>
        <a v-else class="display_flex">
          <h3
            class="
              flex
              h-10
              w-10
              flex-shrink-0
              items-center
              justify-center
              rounded-full
              text-white
              mt-1
              bg-[#ffe4c5]
            "
          >
            {{ step }}
          </h3>
          <h4 v-if="step === 1" class="ml-4 mt-3 text-[#FF8A00]">Delivery</h4>
          <div v-if="step === 1">
            <svg
              class="w-2 text-[#FF8A00] ml-8 mt-2.5"
              viewBox="0 0 22 80"
              fill="none"
              preserveAspectRatio="none"
            >
              <path
                d="M0 -2L20 40L0 82"
                vector-effect="non-scaling-stroke"
                stroke="currentcolor"
                stroke-linejoin="round"
              />
            </svg>
          </div>
          <h4 v-if="step === 2" class="ml-4 mt-3 text-[#FF8A00]">Payment</h4>
          <div v-if="step === 2">
            <svg
              class="w-2 text-[#FF8A00] ml-8 mt-2.5"
              viewBox="0 0 22 80"
              fill="none"
              preserveAspectRatio="none"
            >
              <path
                d="M0 -2L20 40L0 82"
                vector-effect="non-scaling-stroke"
                stroke="currentcolor"
                stroke-linejoin="round"
              />
            </svg>
          </div>
          <h4 v-if="step === 3" class="ml-4 mt-3 text-[#FF8A00]">Finish</h4>
        </a>
      </div>
    </div>
    <div class="container bg-white">
      <form @submit.prevent="handleSubmit" class="checkout-form">
        <div class="row">
          <div class="col-8"></div>
          <div class="col-4"></div>
        </div>
        <div class="grid-container">
          <div class="container_content">
            <div v-if="currentStep === 1">
              <div
                class="
                  flex
                  justify-between
                  align-center
                  pt-12
                  text-[#ff8a00]
                  pl-3
                "
              >
                <div>
                  <h1 class="text-3xl mt-3">Delivery Details</h1>
                </div>

                <div class="relative flex items-start mt-5">
                  <div class="flex h-5 items-center">
                    <input
                      aria-describedby="comments-description"
                      name="comments"
                      type="checkbox"
                      id="name"
                      value="name"
                      v-model="isDropshipper"
                      class="
                        h-4
                        w-4
                        rounded
                        border-gray-300
                        text-indigo-600
                        focus:ring-indigo-500
                      "
                    />
                  </div>
                  <div class="ml-3 text-md">
                    <label for="comments" class="font-medium text-gray-700"
                      >Send as Dropshipper</label
                    >
                    <span id="comments-description" class="text-gray-500"
                      ><span class="sr-only">Send as dropshipper</span></span
                    >
                  </div>
                </div>
              </div>
              <div class="grid-container__content mt-14 ml-10 text-left">
                <div>
                  <Input label="Email" v-model:inputVal="email" />
                  <Input label="Phone Number" v-model:inputVal="phone" />
                  <Input
                    label="Delivery Address"
                    v-model:inputVal="deliveryAddress"
                    type="textArea"
                  />
                </div>
                <div>
                  <Input
                    label="Dropshipper Name"
                    v-model:inputVal="name"
                    isRequired="false"
                  />
                  <Input
                    label="Dropshipper Phone Number"
                    v-model:inputVal="phone"
                    isRequired="false"
                  />
                </div>
              </div>
            </div>
            <div v-if="currentStep === 2">
              <div class="title__container text-[#FF8A00] pl-3 text-3xl mt-3">
                <div>
                  <h1>Shipment</h1>
                </div>
              </div>
              <div class="grid-container__content">
                <div>
                  <div class="display_flex">
                    <Payment
                      :class="
                        selectedBox === i.price ? 'selected' : 'not-selected'
                      "
                      @click="setValue(i.price)"
                      v-for="i in listBox"
                      v-model:name="i.name"
                      v-bind:key="i"
                      v-model:price="i.price"
                    />
                  </div>
                </div>
              </div>
              <div class="title__container text-[#FF8A00] pl-3 text-3xl mt-3">
                <div>
                  <h1>Payment</h1>
                </div>
              </div>
              <div class="grid-container__content">
                <div>
                  <div class="display_flex">
                    <Payment
                      :class="
                        selectedBoxPayment === i.name
                          ? 'selected'
                          : 'not-selected'
                      "
                      @click="setValuePayment(i.name)"
                      v-for="i in listBoxPayment"
                      v-model:name="i.name"
                      v-bind:key="i"
                    />
                  </div>
                </div>
              </div>
            </div>
            <div v-if="currentStep === 3">
              <div
                class="text-[#FF8A00] pl-3 mt-24 place-content-center text-md"
                style="place-contenta: center"
              >
                <div>
                  <h1>Thankyou</h1>
                  <h1>Order ID {{ makeRandomString }}</h1>
                  <P>Your order will be delivered today with JNE</P>
                </div>
              </div>
            </div>
          </div>

          <div class="container__summary h-1/5">
            <div class="container__summary_summary mt-10">
              <h3 class="summary text-[#FF8A00]">Summary</h3>
              <p>10 Items purchased</p>
            </div>

            <div class="display_flex space_between pr-2">
              <p>Cost of Goods</p>
              <p>
                <b>500,000</b>
              </p>
            </div>

            <div v-if="isDropshipper" class="display_flex space_between pr-2">
              <p>Dropshipping Fee</p>
              <p>
                <b>5,900</b>
              </p>
            </div>
            <div
              class="display_flex space_between pr-2"
              v-if="currentStep === 2"
            >
              <h2>Shipment</h2>
              <h2>{{ selectedBox }}</h2>
            </div>
            <div class="display_flex space_between pr-2 text-[#FF8A00]">
              <h2>Total</h2>
              <h2>
                <!-- {{ totalAmount }} -->
                {{ isDropshipper ? "505,900" : "500,000" }}
              </h2>
            </div>

            <div class="address__field mt-7">
              <button type="submit" class="bg-[#FF8A00] text-white">
                Continue to Payment
              </button>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";
import Input from "./components/Input.vue";
import Payment from "./components/Payment.vue";
export default {
  name: "CheckoutForm",
  data: function () {
    return {
      steps: 3,
      currentStep: 1,
      isDropshipper: false,
      // totalAmount: "",
      selectedBox: "",
      selectedBoxPayment: "",
      listBox: [
        {
          name: "GO-SEND",
          price: 15000,
        },
        {
          name: "JNE",
          price: 9000,
        },
        {
          name: "Personal Courier",
          price: 29000,
        },
      ],
      listBoxPayment: [
        {
          name: "E-Wallet",
        },
        {
          name: "Bank Transfer",
        },
        {
          name: "Virtual Account",
        },
      ],
    };
  },
  components: {
    Input,
    Payment,
  },
  methods: {
    handleSubmit() {
      this.currentStep += 1;
    },
    backToHome() {
      this.currentStep = 1;
    },
    setValue(val) {
      this.selectedBox = val;
    },
    setValuePayment(val) {
      this.shipping = val;
      this.selectedBoxPayment = val;
    },
  },
  computed: {
    makeRandomString() {
      let text = "";
      const possible = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
      for (let i = 0; i < 5; i++)
        text += possible.charAt(Math.floor(Math.random() * possible.length));

      return text;
    },
    // totalAmount() {
    //   this.isDropshipper + 500000 + this.selectedBox;
    //   console.log(this.totalAmount);
    // },
  },
  setup() {
    const form = reactive({
      dropshipperName: "",
      email: "",
      phone: "",
      deliveryAddress: "",
      dropshipperPhone: "",
    });
    return {
      form,
    };
  },
};
</script>
<style lang="scss">
@import "./assets/main.scss";
.app {
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background-color: #fffae6;
}

.container__step {
  position: absolute;
  z-index: 1000;
  display: flex;
  width: 40vw;
  height: 5vw;
  justify-content: space-around;
  top: 5%;
  border-radius: 35px;
}
</style>
