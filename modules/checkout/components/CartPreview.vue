<template>
  <div>
    <div class="highlighted">
      <SfHeading
        :level="3"
        :title="$t('Order summary')"
        class="sf-heading--left sf-heading--no-underline title"
      />
    </div>
    <div class="highlighted">
      <SfProperty
        :name="$t('Products')"
        :value="totalItems"
        class="sf-property--full-width sf-property--large property"
      />
      <SfProperty
        :name="$t('Subtotal')"
        :value="$fc(totals.subtotal)"
        :class="['sf-property--full-width', 'sf-property--large property']"
      />
 
      <SfProperty
        :name="$t('Tax')"
        :value="taxAmount.toFixed(2)"
        class="sf-property--full-width sf-property--large property"
      />
      <!-- <SfProperty
        v-if="hasDiscounts"
        :name="$fc(discount)"
        :value="$fc(discount)"
        class="sf-property--full-width sf-property--small property"
      /> -->
      <div class="sf-property--full-width sf-property--large property sf-property">
          <span class="sf-property__name discount_label_checkout" v-for="(d, index) in discount" :key="index">{{ d.name }}</span>
          <span class="sf-property__value" v-for="(d, index) in discount" :key="index">
            -₹{{ d.value | currency }}
          </span>
      </div>
      <SfProperty
        v-if="selectedShippingMethod"
        :name="$t('Shipping')"
        :value="$fc(getShippingMethodPrice(selectedShippingMethod))"
        class="sf-property--full-width sf-property--large property"
      />

      <SfProperty
        :name="$t('Total')"
        :value="$fc(totals.total)"
        class="sf-property--full-width sf-property--large property-total"
      />

      <p class="gst_info" id='out_maha'>
        (includes  <span>₹{{ taxAmount.toFixed(2) }} </span> IGST )
      </p>
      <p class="gst_info" id="in_maha">
        (includes <span>₹{{ cgst_igst_amount.toFixed(2) }}</span> CGST, &nbsp; <span>₹{{ cgst_igst_amount.toFixed(2) }}</span> SGST)
      </p>

    </div>
    <CouponCode class="highlighted" />
    <!-- <div class="highlighted">
      <SfCharacteristic
        v-for="characteristic in characteristics"
        :key="characteristic.title"
        :title="characteristic.title"
        :description="characteristic.description"
        :icon="characteristic.icon"
        class="characteristic"
      />
    </div> -->
  </div>
</template>
<script lang="ts">
import { SfHeading, SfProperty, SfCharacteristic } from '@storefront-ui/vue';
import { computed, ref, defineComponent } from '@nuxtjs/composition-api';
import cartGetters from '~/modules/checkout/getters/cartGetters';
import useCart from '~/modules/checkout/composables/useCart';
import getShippingMethodPrice from '~/helpers/checkout/getShippingMethodPrice';
import CouponCode from '../../../components/CouponCode.vue';

const CHARACTERISTICS = [
  {
    title: 'Safety',
    description: 'It carefully packaged with a personal touch',
    icon: 'safety',
  },
  {
    title: 'Easy shipping',
    description: 'You’ll receive dispatch confirmation and an arrival date',
    icon: 'shipping',
  },
  {
    title: 'Changed your mind?',
    description: 'Rest assured, we offer free returns within 30 days',
    icon: 'return',
  },
];

export default defineComponent({
  name: 'CartPreview',
  components: {
    SfHeading,
    SfProperty,
    SfCharacteristic,
    CouponCode,
  },
  setup() {
    const { cart, removeItem, updateItemQty } = useCart();

    const listIsHidden = ref(false);

    const products = computed(() => cartGetters.getItems(cart.value));
    const totalItems = computed(() => cartGetters.getTotalItems(cart.value));
    const totals = computed(() => cartGetters.getTotals(cart.value));
    // const totals = computed(() => {
    //   const baseTotal = cartGetters.getTotals(cart.value).total; // Original total from cart
    //   const shippingCost = selectedShippingMethod.value
    //     ? getShippingMethodPrice(selectedShippingMethod.value)
    //     : 0; // Get the shipping cost or default to 0
    //   return {
    //     ...cartGetters.getTotals(cart.value),
    //     total: baseTotal + shippingCost, // Add the shipping cost to the total
    //   };
    // });

    // const discount = computed(() => -cartGetters.getDiscountAmount(cart.value));
    const discount = computed(() => {
      const discounts = cartGetters.getDiscounts(cart.value);
      return discounts.map((d) => ({
        name: d.name, // Pass the discount name
        value: d.value, // Pass the discount amount
      }));
    });
    // const hasDiscounts = computed(() => Math.abs(discount.value) > 0);
    const selectedShippingMethod = computed(() => cartGetters.getSelectedShippingMethod(cart.value));
    const taxAmount = computed(() => cartGetters.getTaxAmount(cart.value)); // Add this line to get the tax amount

    const cgst_igst_amount = computed(() => {
      const tax = taxAmount.value;
      return typeof tax === 'number' ? tax / 2 : 0;
    });

    return {
      cart,
      discount,
      // hasDiscounts,
      totalItems,
      listIsHidden,
      products,
      totals,
      removeItem,
      updateItemQty,
      cartGetters,
      getShippingMethodPrice,
      characteristics: CHARACTERISTICS,
      selectedShippingMethod,
      taxAmount,
      cgst_igst_amount,
    };
  },
});
</script>
<style>
.discount_label_checkout {
  width:60%;
}
.highlighted span {
  font-family: 'Montserrat' !important;
}
input#couponCode {
  border: 1px solid #a18e11;
  width: 92%;
  height: 32px;
}
button.coupon-code__button.sf-button {
    font-family: 'Montserrat';
    font-weight: 400;
}
.gst_info {
    display: none;
    margin: 0;
    margin-top: 10px;
    font-size: 13px;
    font-family: 'Raleway';
}
.gst_info span {
    font-size: 20px;
}
</style>
<style lang="scss" scoped>
.highlighted {
  box-sizing: border-box;
  width: 100%;
  background-color: var(--c-light);
  padding: var(--spacer-xl) var(--spacer-xl) 0;

  &:last-child {
    padding-bottom: var(--spacer-xl);
  }
}

.total-items {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: var(--spacer-xl);
}

.property {
  margin-bottom: var(--spacer-base);
}

.property-total {
  margin-top: var(--spacer-xl);
  padding-top: var(--spacer-lg);
  font-size: var(--font-size-xl);
  border-top: var(--c-white) 1px solid;
  --property-name-font-weight: var(--font-weight--semibold);
  --property-name-color: var(--c-text);
}

.characteristic {
  &:not(:last-child) {
    margin-bottom: var(--spacer-base);
  }
}
</style>
