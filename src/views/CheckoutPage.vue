<template>
  <div class="checkout-page">
    <div class="container py-4">
      <h2 class="mb-4">Checkout</h2>

      <div class="row">
        <div class="col-lg-8 mb-4">
          <!-- Shipping Information -->
          <div class="card border-0 shadow-sm mb-4">
            <div class="card-body">
              <h5 class="mb-4">Shipping Information</h5>

              <form @submit.prevent="handleSubmit">
                <div class="row">
                  <div class="col-md-6 mb-3">
                    <label class="form-label">First Name *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.firstName"
                      required
                    />
                  </div>

                  <div class="col-md-6 mb-3">
                    <label class="form-label">Last Name *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.lastName"
                      required
                    />
                  </div>

                  <div class="col-12 mb-3">
                    <label class="form-label">Phone Number *</label>
                    <input
                      type="tel"
                      class="form-control"
                      v-model="formData.phone"
                      required
                    />
                  </div>

                  <div class="col-12 mb-3">
                    <label class="form-label">Email *</label>
                    <input
                      type="email"
                      class="form-control"
                      v-model="formData.email"
                      required
                    />
                  </div>

                  <div class="col-12 mb-3">
                    <label class="form-label">Address *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.address"
                      required
                    />
                  </div>

                  <div class="col-md-6 mb-3">
                    <label class="form-label">City *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.city"
                      required
                    />
                  </div>

                  <div class="col-md-6 mb-3">
                    <label class="form-label">Postal Code *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.postalCode"
                      required
                    />
                  </div>

                  <div class="col-12 mb-3">
                    <label class="form-label">Order Notes (Optional)</label>
                    <textarea
                      class="form-control"
                      rows="3"
                      v-model="formData.notes"
                    ></textarea>
                  </div>
                </div>
              </form>
            </div>
          </div>

          <!-- Payment Method -->
          <div class="card border-0 shadow-sm">
            <div class="card-body">
              <h5 class="mb-4">Payment Method</h5>

              <div class="form-check mb-3">
                <input
                  class="form-check-input"
                  type="radio"
                  name="payment"
                  id="cod"
                  value="cod"
                  v-model="formData.paymentMethod"
                />
                <label class="form-check-label" for="cod">
                  <i class="bi bi-cash me-2"></i>
                  Cash on Delivery
                </label>
              </div>

              <div class="form-check mb-3">
                <input
                  class="form-check-input"
                  type="radio"
                  name="payment"
                  id="card"
                  value="card"
                  v-model="formData.paymentMethod"
                />
                <label class="form-check-label" for="card">
                  <i class="bi bi-credit-card me-2"></i>
                  Credit / Debit Card
                </label>
              </div>

              <div
                v-if="formData.paymentMethod === 'card'"
                class="card-details mt-3 p-3 bg-light rounded"
              >
                <div class="row">
                  <div class="col-12 mb-3">
                    <label class="form-label">Card Number *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.cardNumber"
                      placeholder="1234 5678 9012 3456"
                      maxlength="19"
                      required
                    />
                  </div>
                  <div class="col-12 mb-3">
                    <label class="form-label">Cardholder Name *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.cardName"
                      placeholder="John Doe"
                      required
                    />
                  </div>
                  <div class="col-6 mb-3">
                    <label class="form-label">Expiry Date *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.cardExpiry"
                      placeholder="MM/YY"
                      maxlength="5"
                      required
                    />
                  </div>
                  <div class="col-6 mb-3">
                    <label class="form-label">CVV *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.cardCvv"
                      placeholder="123"
                      maxlength="3"
                      required
                    />
                  </div>
                </div>
              </div>

              <div class="form-check">
                <input
                  class="form-check-input"
                  type="radio"
                  name="payment"
                  id="bank"
                  value="bank"
                  v-model="formData.paymentMethod"
                />
                <label class="form-check-label" for="bank">
                  <i class="bi bi-bank me-2"></i>
                  Bank Transfer
                </label>
              </div>

              <div
                v-if="formData.paymentMethod === 'bank'"
                class="bank-details mt-3 p-3 bg-light rounded"
              >
                <div class="row">
                  <div class="col-12 mb-3">
                    <label class="form-label">Bank Name *</label>
                    <select
                      class="form-select"
                      v-model="formData.bankName"
                      required
                    >
                      <option value="">Select Bank</option>
                      <option value="bank1">National Bank</option>
                      <option value="bank2">Commercial Bank</option>
                      <option value="bank3">International Bank</option>
                      <option value="bank4">City Bank</option>
                    </select>
                  </div>
                  <div class="col-12 mb-3">
                    <label class="form-label">Account Number *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.accountNumber"
                      placeholder="Enter your account number"
                      required
                    />
                  </div>
                  <div class="col-12 mb-3">
                    <label class="form-label">Account Holder Name *</label>
                    <input
                      type="text"
                      class="form-control"
                      v-model="formData.accountHolder"
                      placeholder="Enter account holder name"
                      required
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="col-lg-4">
          <div class="card border-0 shadow-sm">
            <div class="card-body">
              <h5 class="mb-4">Order Summary</h5>

              <div class="order-items mb-3">
                <div
                  v-for="item in cartItems"
                  :key="item.id"
                  class="d-flex justify-content-between mb-2"
                >
                  <span>{{ item.name }} × {{ item.quantity }}</span>
                  <span>${{ item.price * item.quantity }}</span>
                </div>
              </div>

              <hr />

              <div class="d-flex justify-content-between mb-2">
                <span>Subtotal:</span>
                <span>${{ cartTotal }}</span>
              </div>

              <div class="d-flex justify-content-between mb-2">
                <span>Shipping:</span>
                <span class="text-success">Free</span>
              </div>

              <div class="d-flex justify-content-between mb-2">
                <span>Tax (15%):</span>
                <span>${{ tax }}</span>
              </div>

              <hr />

              <div class="d-flex justify-content-between mb-4">
                <span class="fw-bold">Total:</span>
                <span class="fw-bold text-primary h5 mb-0"
                  >${{ totalWithTax }}</span
                >
              </div>

              <button
                class="btn btn-primary w-100 mb-3"
                @click="handleSubmit"
                :disabled="!isFormValid"
              >
                Confirm Order
              </button>

              <div class="text-center">
                <small class="text-muted">
                  <i class="bi bi-shield-check me-1"></i>
                  Secure and encrypted transaction
                </small>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import { useRouter } from "vue-router";
import { useCartStore } from "../store/cartStore";

const router = useRouter();
const cartStore = useCartStore();

const formData = ref({
  firstName: "",
  lastName: "",
  phone: "",
  email: "",
  address: "",
  city: "",
  postalCode: "",
  notes: "",
  paymentMethod: "cod",
  cardNumber: "",
  cardName: "",
  cardExpiry: "",
  cardCvv: "",
  bankName: "",
  accountNumber: "",
  accountHolder: "",
});

const cartItems = computed(() => cartStore.items);
const cartTotal = computed(() => cartStore.cartTotal);
const tax = computed(() => Math.round(cartTotal.value * 0.15));
const totalWithTax = computed(() => cartTotal.value + tax.value);

const isFormValid = computed(() => {
  const basicValid =
    formData.value.firstName &&
    formData.value.lastName &&
    formData.value.phone &&
    formData.value.email &&
    formData.value.address &&
    formData.value.city &&
    formData.value.postalCode &&
    formData.value.paymentMethod;

  if (!basicValid) return false;

  if (formData.value.paymentMethod === "card") {
    return (
      formData.value.cardNumber &&
      formData.value.cardName &&
      formData.value.cardExpiry &&
      formData.value.cardCvv
    );
  }

  if (formData.value.paymentMethod === "bank") {
    return (
      formData.value.bankName &&
      formData.value.accountNumber &&
      formData.value.accountHolder
    );
  }

  return true;
});

const handleSubmit = async () => {
  if (!isFormValid.value) {
    alert("Please fill in all required fields");
    return;
  }

  try {
    const orderDate = new Date().toISOString();

    const buyerData = {
      firstName: formData.value.firstName,
      lastName: formData.value.lastName,
      fullName: `${formData.value.firstName} ${formData.value.lastName}`,
      phone: formData.value.phone,
      email: formData.value.email,
      address: formData.value.address,
      city: formData.value.city,
      postalCode: formData.value.postalCode,
      notes: formData.value.notes,
      paymentMethod: formData.value.paymentMethod,
      orderDate: orderDate,
    };

    const salesData = {
      items: cartItems.value.map((item) => ({
        id: item.id,
        name: item.name,
        price: item.price,
        quantity: item.quantity,
        total: item.price * item.quantity,
      })),
      subtotal: cartTotal.value,
      tax: tax.value,
      total: totalWithTax.value,
      orderDate: orderDate,
    };

    const buyerResponse = await fetch(
      "https://electronics-store-c9093-default-rtdb.firebaseio.com/Buyers.json",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(buyerData),
      }
    );

    if (!buyerResponse.ok) {
      throw new Error("Failed to save buyer data");
    }

    const salesResponse = await fetch(
      "https://electronics-store-c9093-default-rtdb.firebaseio.com/Sales.json",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(salesData),
      }
    );

    if (!salesResponse.ok) {
      throw new Error("Failed to save sales data");
    }

    const buyerResult = await buyerResponse.json();
    const salesResult = await salesResponse.json();

    console.log("Buyer saved with ID:", buyerResult.name);
    console.log("Sales saved with ID:", salesResult.name);

    // Success
    alert(
      "Your order has been confirmed successfully! We will contact you soon"
    );
    cartStore.clearCart();
    router.push("/");
  } catch (error) {
    console.error("Error saving order:", error);
    alert("There was an error processing your order. Please try again.");
  }
};
</script>

<style scoped>
.order-items {
  max-height: 200px;
  overflow-y: auto;
}

.form-check-input:checked {
  background-color: #667eea;
  border-color: #667eea;
}

.card-details,
.bank-details {
  animation: slideDown 0.3s ease-out;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
