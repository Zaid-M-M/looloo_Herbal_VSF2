<template>
  <div class="checkout_main">
    <div id="checkout">
      <div class="checkout">
        <div class="checkout__main">
          <SfSteps
            v-if="!isThankYou"
            :active="currentStepIndex"
            :class="{ checkout__steps: true }"
            @change="handleStepClick"
          >
            <SfStep
              v-for="(step, key) in STEPS"
              :key="key"
              :name="$t(step.title)"
              :active="1"
              can-go-back
            >
              <nuxt-child />
            </SfStep>
          </SfSteps>
          <nuxt-child v-else />
        </div>
        <div
          v-if="!isThankYou"
          class="checkout__aside desktop-only"
        >
          <transition name="fade">
            <CartPreview key="order-summary" />
          </transition>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { SfSteps } from '@storefront-ui/vue';
import {
  computed,
  defineComponent,
  ref,
  useRoute,
  useRouter,
  useContext,
  onMounted,
} from '@nuxtjs/composition-api';
import cartGetters from '~/modules/checkout/getters/cartGetters';
import useCart from '~/modules/checkout/composables/useCart';
import CartPreview from '~/modules/checkout/components/CartPreview.vue';

export default defineComponent({
  name: 'CheckoutPage',
  components: {
    SfSteps,
    CartPreview,
  },
  setup() {
    const route = useRoute();
    const { app } = useContext();
    const { path } = route.value;
    const router = useRouter();
    const { cart, load } = useCart();
    const products = computed(() => cartGetters.getItems(cart.value));
    const currentStep = computed(() => path.split('/').pop());

    const STEPS = ref([
      {
        title: 'User Account',
        url: 'user-account',
      },
      {
        title: 'Shipping',
        url: 'shipping',
      },
      {
        title: 'Billing',
        url: 'billing',
      },
      {
        title: 'Payment',
        url: 'payment',
      },
    ]);

    const currentStepIndex = computed(() => STEPS.value.findIndex((step) => step.url === currentStep.value));
    const isThankYou = computed(() => currentStep.value === 'thank-you');

    const handleStepClick = async (stepIndex: number) => {
      if (stepIndex <= currentStepIndex.value) {
        const { url } = STEPS.value[stepIndex];
        await router.push(`${app.localePath(`/checkout/${url}`)}`);
      }
    };

    onMounted(async () => {
      await load();
      if (products.value.length === 0 && currentStep.value !== 'thank-you') {
        await router.push(app.localePath('/'));
      }
    });

    return {
      handleStepClick,
      STEPS,
      currentStepIndex,
      isThankYou,
      currentStep,
    };
  },
});
</script>

<style>
.checkout_main {
    background-color: #f5f1dd;
}
.checkout {
    padding: 50px 0;
}
.sf-steps__header {
    border-color: #978d4b69;
}
@media (min-width: 1024px) {
  .sf-steps__step::after {
    bottom: -4.52px;
    width: 7px;
    height: 7px;
  }
}
.checkout_main .sf-heading__title.h3 {
    color: #a18e11;
    font-weight: 400 !important;
}
.checkout_main .sf-input input {
  border-color: #a18e11;
  color: #6d6b5d !important;
  font-size: 17px !important;
  font-weight: 400 !important;
}
.sf-input input:focus {
  outline: none;
}
.sf-input input, h1,h2, h3 , h4 , p ,a , label , span.sf-checkbox__label ,
.sf-radio__label.shipping__label div , .shipping__info , .checkout_main div , .checkout_main span 
.checkout_main th , .checkout_main td{
  font-family: 'Montserrat' !important;
}
select#Country , select#State\/Province{
    background: transparent;
    border-color: #a18e11;
    font-family: 'Montserrat' !important;
    color: #6d6b5d !important;
}
.highlighted {
  background-color: #fff !important;
}
.checkout_main tr.sf-table__row , .checkout_main  .sf-divider{
    border-color: #dfd8b5;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 767px) {
  button.sf-steps__step {
    font-size: 14px;
    line-height: 19px;
  }
}
</style>

<style lang="scss" scoped>
#checkout {
  box-sizing: border-box;
  @include for-desktop {
    max-width: 1240px;
    margin: 0 auto;
    padding: 0 1.5rem;
  }
}

.checkout {
  @include for-desktop {
    display: flex;
  }

  &__main {
    @include for-desktop {
      flex: 1;
      padding: var(--spacer-xl) 0 0 0;
    }
  }

  &__aside {
    @include for-desktop {
      flex: 0 0 25.5rem;
      margin: 0 0 0 4.25rem;
    }
  }

  &__steps {
    --steps-content-padding: 0 var(--spacer-base);
    @include for-desktop {
      --steps-content-padding: 0;
    }

    &-auth::v-deep .sf-steps__step:first-child {
      --steps-step-color: #e8e4e4;
    }
  }
}
</style>
