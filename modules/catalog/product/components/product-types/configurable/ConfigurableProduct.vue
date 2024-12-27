<template>
  <div>
    <div class="product">
      <SfLoader
        class="loading--product-gallery"
        :loading="isFetching"
      >
        <SfGallery
          :images="productGallery"
          :image-width="imageSizes.productGallery.imageWidth"
          :image-height="imageSizes.productGallery.imageHeight"
          :thumb-width="imageSizes.productGallery.thumbWidth"
          :thumb-height="imageSizes.productGallery.thumbHeight"
          :enable-zoom="true"
          image-tag="nuxt-img"
          thumb-image-tag="nuxt-img"
          class="product__gallery"
          :nuxt-img-config="{
            fit: 'cover',
          }"
          :thumb-nuxt-img-config="{
            fit: 'cover',
          }"
        />
      </SfLoader>
      <div class="product__info">
        <div class="product__header">
          <SfHeading
            :title="getProductName(product)"
            :level="3"
            class="sf-heading--no-underline sf-heading--left"
          />
          <SvgImage
            icon="drag"
            width="40"
            height="40"
            class="product__drag-icon smartphone-only"
          />
        </div>
        <div class="product__price-and-rating">
          <SfPrice
            :regular="$fc(productPrice)"
            :special="productSpecialPrice && $fc(productSpecialPrice)"
          />
          <div>
            <div class="product__rating">
              <SfRating
                :score="averageRating"
                :max="5"
              />
              <a
                v-if="!!totalReviews"
                href="#"
                class="product__count"
              >
                ({{ totalReviews }})
              </a>
            </div>
            <SfButton
              class="sf-button--text"
              @click="setActiveTab(TabsConfig.reviews.ID)"
            >
              {{ $t('Read all reviews') }}
            </SfButton>
            |
            <SfButton
              class="sf-button--text"
              @click="openNewReviewTab"
            >
              {{ $t('Add a review') }}
            </SfButton>
          </div>
        </div>
        <div v-if="product !== null ">
          
          <template v-for="option in configurableOptions">
            <div
              v-if="option.attribute_code === 'color'"
              :key="option.uid"
              class="product__colors"
            >
              <p class="product__color-label">
                {{ option.label }}:
              </p>
              <SfColor
                v-for="color in option.values"
                :key="color.uid"
                :color="getProductSwatchData(color.swatch_data)"
                :color-uid="color.uid"
                :selected="
                  productConfiguration[option.attribute_uid] === color.uid
                "
                class="product__color"
                @click="
                  () =>
                    updateProductConfiguration(
                      option.attribute_uid,
                      color.uid
                    )
                "
              />
            </div>
            <SfSelect
              v-else
              :key="option.uid"
              :value="productConfiguration[option.attribute_uid]"
              :label="option.label"
              class="sf-select--underlined product__select-size"
              :required="true"
              @input="
                ($event) =>
                  updateProductConfiguration(option.attribute_uid, $event)
              "
            >
              <SfSelectOption :value="''" />
              <SfSelectOption
                v-for="attribute in option.values"
                :key="attribute.uid"
                :value="attribute.uid"
              >
                {{ attribute.label }}
              </SfSelectOption>
            </SfSelect>
          </template>
          <SfAddToCart
            v-model="qty"
            v-e2e="'product_add-to-cart'"
            :disabled="isCartLoading || !canAddToCart(product, qty) || isFetching"
            class="product__add-to-cart"
          >
            <template #add-to-cart-btn>
              <SfButton
                class="sf-add-to-cart__button"
                :disabled="isCartLoading || !canAddToCart(product, qty) || isFetching"
                @click="addItem({ product, quantity: parseInt(qty), productConfiguration })"
              >
                {{ $t('Add to cart') }}
              </SfButton>
            </template>
          </SfAddToCart>

          <HTMLContent
            v-if="productShortDescription"
            :content="productShortDescription"
            tag="p"
            class="product__description desktop-only"
          />

          <SfAlert
            :style="{ visibility: !!addToCartError ? 'visible' : 'hidden'}"
            class="product__add-to-cart-error"
            :message="$t(addToCartError)"
            type="danger"
          />
          <div class="product__additional-actions">
            <AddToWishlist
              :is-in-wishlist="isInWishlist"
              :is-show="isAuthenticated"
              @addToWishlist="addItemToWishlist({product})"
            />
          </div>
        </div>
       
      </div>
    </div>

    <LazyHydrate when-idle>
            <ProductTabs
              :product="product"
              :open-tab="activeTab"
              :key-ingredients="keyIngredients"
              :benefits="benefits"
              :method_of_use="method_of_use"
              @changeTab="setActiveTab($event)"
            />
        </LazyHydrate>

  </div>
</template>
<script lang="ts">
import LazyHydrate from 'vue-lazy-hydration';
import {
  SfAddToCart,
  SfButton,
  SfColor,
  SfGallery,
  SfHeading,
  SfLoader,
  SfPrice,
  SfRating,
  SfSelect,
  SfAlert,
} from '@storefront-ui/vue';
import {
  ref,
  computed,
  useContext,
  useRoute,
  useRouter,
  onMounted,
  defineComponent,
  PropType, toRef,
} from '@nuxtjs/composition-api';

import {
  getSwatchData as getProductSwatchData,
  getName as getProductName,
} from '~/modules/catalog/product/getters/productGetters';

import {
  getTotalReviews,
  getAverageRating,
} from '~/modules/review/getters/reviewGetters';

import { useCart } from '~/modules/checkout/composables/useCart';
import useWishlist from '~/modules/wishlist/composables/useWishlist';
import SvgImage from '~/components/General/SvgImage.vue';
import HTMLContent from '~/components/HTMLContent.vue';
import AddToWishlist from '~/components/AddToWishlist.vue';
import { useUser } from '~/modules/customer/composables/useUser';
import { getConfigurableProductPriceCommand } from '~/modules/catalog/pricing/getConfigurableProductPriceCommand';
import { getConfigurableProductSpecialPriceCommand } from '~/modules/catalog/pricing/getConfigurableProductSpecialPriceCommand';
import { Product } from '~/modules/catalog/product/types';
import ProductTabs from '~/modules/catalog/product/components/tabs/ProductTabs.vue';
import { useProductGallery } from '~/modules/catalog/product/composables/useProductGallery';
import { TabsConfig, useProductTabs } from '~/modules/catalog/product/composables/useProductTabs';
import { usePageStore } from '~/stores/page';
import axios from 'axios';

export default defineComponent({
  name: 'ConfigurableProduct',
  components: {
    HTMLContent,
    LazyHydrate,
    SfAddToCart,
    SfButton,
    SfColor,
    SfGallery,
    SfHeading,
    SfLoader,
    SfPrice,
    SfRating,
    SfSelect,
    SfAlert,
    AddToWishlist,
    SvgImage,
    ProductTabs,
  },
  transition: 'fade',
  props: {
    product: {
      type: [Object, null] as PropType<Product>,
      default: null,
    },
    isFetching: {
      type: Boolean,
      default: true,
    },
  },
  setup(props, { emit }) {
    const qty = ref(1);
    const product = toRef(props, 'product');
    const route = useRoute();
    const router = useRouter();
    const { routeData } = usePageStore();
    const {
      addItem, error: cartError, loading: isCartLoading, canAddToCart,
    } = useCart();
    const { productGallery, imageSizes } = useProductGallery(product);
    const { activeTab, setActiveTab, openNewReviewTab } = useProductTabs();

    const { isAuthenticated } = useUser();
    const { addOrRemoveItem, isInWishlist } = useWishlist();
    const { app } = useContext();

    const productShortDescription = computed(
      () => props.product?.short_description?.html || '',
    );

    // Define reactive state for key ingredients
    const keyIngredients = ref('');
    const benefits = ref('');
    const method_of_use = ref('');


    // Fetch product data including key_ingredients using REST API
    const fetchProductData = async (sku: string) => {
      try {
        const response = await axios.get(`https://magento-722835-4834193.cloudwaysapps.com/rest/V1/products/${sku}`);
        const productData = response.data;

        // Find key_ingredients in custom attributes
        const keyIngredientsAttribute = productData.custom_attributes.find((attr: any) => attr.attribute_code === 'key_ingredients');
        keyIngredients.value = keyIngredientsAttribute ? keyIngredientsAttribute.value : '';

        const benefitsAttribute = productData.custom_attributes.find((attr: any) => attr.attribute_code === 'benefits');
        benefits.value = benefitsAttribute ? benefitsAttribute.value : '';

        const method_of_useAttribute = productData.custom_attributes.find((attr: any) => attr.attribute_code === 'method_of_use');
        method_of_use.value = method_of_useAttribute ? method_of_useAttribute.value : '';
        
      } catch (error) {
        console.error('Error fetching product data:', error);
      }
    };

    // Fetch data on component mount
    onMounted(() => {
      if (product.value) {
        fetchProductData(product.value.sku);
      }
    });

    const configurableOptions = computed(
      () => props.product?.configurable_options ?? [],
    );

    const productConfiguration = ref(route.value.query);
    const productPrice = computed(() => getConfigurableProductPriceCommand(props.product));
    const productSpecialPrice = computed(() => getConfigurableProductSpecialPriceCommand(props.product));

    const getBaseSearchQuery = () => ({
      filter: {
        sku: {
          eq: routeData.sku,
        },
      },
      configurations: Object.entries(productConfiguration.value).map(
        (config) => config[1],
      ) as string[],
    });

    const totalReviews = computed(() => getTotalReviews(props.product));
    const averageRating = computed(() => getAverageRating(props.product));
    const addToCartError = computed(() => cartError.value?.addItem?.message);
    const updateProductConfiguration = (label: string, value: string) => {
      if (productConfiguration.value[label] === value) return;

      productConfiguration.value[label] = value;
      const routerData = router.resolve({
        path: `${app.localePath(window.location.pathname)}`,
        query: {
          ...productConfiguration.value,
        },
      });

      window.history.pushState({}, null, routerData.href);

      emit('fetchProduct', { query: getBaseSearchQuery() });
    };

    return {
      keyIngredients,
      benefits,
      method_of_use,
      addItem,
      addItemToWishlist: addOrRemoveItem,
      canAddToCart,
      configurableOptions,
      updateProductConfiguration,
      isAuthenticated,
      isInWishlist: computed(() => isInWishlist({ product: props.product })),
      isCartLoading,
      productConfiguration,
      productGallery,
      getProductName,
      getProductSwatchData,
      productPrice,
      productShortDescription,
      productSpecialPrice,
      qty,
      totalReviews,
      averageRating,
      imageSizes,
      setActiveTab,
      openNewReviewTab,
      activeTab,
      TabsConfig,
      addToCartError,
    };
  },
});
</script>
<style>
.sf-select.is-selected {
      --select-label-transform: var(--select-label-translate3d, translate3d(0, 0, 0)) !important;
}
.product {
  /* display: block !important;*/
  /* width: 100%;*/
  /* float: left;*/
 padding-top: 70px;
 /* background: blue; */
}
.product .loading--product-gallery {
 width: 40%;
 float: left;
 /* background: green; */
 padding-top: 0px !important;
}
.product .product__info {
 max-width: 55% !important;
 float: left;
 padding-left: 55px !important;
 /* background: aqua; */
}
.product .sf-gallery.product__gallery {
   display: block;
   height:100%;
}
.product .sf-gallery__thumbs {
   display: flex;
   flex-direction: row;
   align-items: flex-start;
   gap:10px;
   height: auto;
}
.product .sf-gallery__thumbs button {
   height: 122px !important;
   max-width: 122px !important;
}
.product .sf-gallery__thumbs button img {
 width: 100%;
}
.product .sf-gallery__stage {
   width: 100%;
   max-width: 100%;
   margin-bottom: 5px;
}

.product .sf-gallery__stage .sf-image--wrapper.sf-gallery__big-image {
 background-color: #fff;
}
.product .sf-gallery__stage .sf-image {
 width: 100%;
 object-fit: contain;
}
.product .product__price-and-rating {
   align-items: flex-end !important;
}
.product h3.sf-heading__title.h3 {
   color: #a18e11;
   font-size: 34px;
   line-height: 44px;
   font-weight: 600;
   font-family: 'Montserrat';
}
.product span.sf-price__regular {
   color: #a18e11;
   font-size: 40px;
   line-height: 30px;
   font-weight: 600;
   font-family: 'Montserrat';
}
.product button.sf-button--text.sf-button {
   font-family: 'Montserrat';
   color: #a18e11;
   font-weight: 600;
}
.product .product__description p {
   font-size: 15px;
   line-height: 25px;
   font-weight: 400;
   font-family: 'Montserrat';
   color: #6d6b5d;
}
.product .product__description p span.skutxt {
   color: #a5a5a5;
}
.sf-add-to-cart__select-quantity.sf-quantity-selector {
   border: 2px solid #a18e11;
   border-radius: 5px;
   background: transparent;
}
.sf-add-to-cart__select-quantity button.sf-quantity-selector__button:first-child {
 border-right: 2px solid #a18e11;
 border-left: 0px solid #a18e11;
}
.sf-add-to-cart__select-quantity button.sf-quantity-selector__button {
 border-left: 2px solid #a18e11;
 font-size: 30px;
 color: #a18e11;
 font-weight: 500;
 padding-top: 0;
 background-color: transparent !important;
}
.sf-input__wrapper input {
   color: #727272;
   font-size: 30px;
   font-weight: 300;
   font-family: 'Montserrat';
}
button.sf-add-to-cart__button.sf-button {
   background-color: #9f9f9f !important;
   text-transform: uppercase;
   border-radius: 5px;
   font-size: 20px;
   width: 178px;
   line-height: 20px;
   font-weight: 300;
   font-family: 'Montserrat';
}
.sf-add-to-cart.product__add-to-cart {
   margin-top: 25px !important;
   margin-left: 0 !important;
   margin-bottom: 42px !important;
}
section.sf-section.section {
 margin-bottom: 0px;
}

div#tabs {
   margin-top: 116px;
   padding-bottom:40px;
   margin-bottom: 0px;
   border-top:1px solid #3333331f;
   border-bottom:1px solid #3333331f;
}
.sf-tabs__content__tab {
   padding-top: 25px;
}
.sf-tabs__title {
 font-family: 'Montserrat';
 font-weight: 300;
 font-size: 15px;
 line-height:25px;
}
.sf-tabs__title:hover {
 color: #a17b20;
}
.sf-tabs__title.is-active {
 border-bottom:0px solid;
 color: #a17b20;
 font-weight: 700;
 border-top:2px solid #a17b20;
}
.sf-tabs__content {
 border:0px;
}
.prd_tabs_main {
   width: 100%;
}
.pt_col {
   width: 22%;
   float: left;
   margin-right: 35px;
   margin-bottom: 15px;
}
.pt_col img {
   width: 100%;
   border: 5px solid #D1CDBD;
}
.pt_col p {
   color: #6d6b5d;
   font-size: 13px;
   line-height: 23px;
   font-family: 'Montserrat';
   font-weight: 400;
}
.pt_col p strong {
   display: block;
}
ul.prd_tab_list {
   margin: 0;
   padding: 0;
   padding-left: 19px;
}
ul.prd_tab_list li {
   color: #6d6b5d;
   font-family: 'Montserrat';
   font-size: 15px;
   line-height: 25px;
   font-weight: 400;
}
.related_prd_slider h2 {
 text-align: left;
 color: #a18e11;
 font-family: 'Montserrat';
 font-size: 24px !important;
 line-height: 34px;
 font-weight: 300 !important;
}
.related_prd_slider .sf-section__content {
   margin-top: 0px;
}



.sf-product-card {
   box-shadow: 0px 0px 4px 0px rgba(58, 44, 12, 0.23137);
   border-radius: 5px;
   padding: 0;
   width: 100% !important;
   max-width: 89%;
   background-color: #eae9c9;
}
span.sf-product-card__title {
   font-size: 15px;
   line-height: 24px;
   color: #a17b20;
   font-family: 'Montserrat';
   text-overflow: unset !important;
   overflow: auto;
   white-space: normal;
   text-align: center;
}
.sf-product-card__price.sf-price {
   justify-content: center;
}
span.sf-price__regular {
   font-size: 20px;
   line-height: 26px;
   color: #a18e11;
   font-family: 'Montserrat';
   font-weight: 400;
}

.product .sf-select {
    margin-top: 45px !important;
}
.product  .sf-select__dropdown {
  width: 250px !important;
  max-width: 100% !important;
  height: 38px;
  font-family: 'Montserrat';
  font-size: 14px;
  line-height: 14px;
  padding: 0 10px !important;
  color: #6d6b5d;
  border-width: 1px;
  border-color: rgba(51, 51, 51, 0.12);
  background-color: #fdfdfd;
  border-radius: 1px;
}
.product .sf-select label.sf-select__label {
  color: #a18e11;
  font-size: 14px;
  font-family: 'Montserrat';
  position: relative;
  top: auto;
  bottom: 5px;
  width: 100%;
  display: block;
  float: left;
  line-height: 0;
}
.product__description h4 {
  padding: 10px;
  text-shadow: 0 1px 2px black;
  color: #ffffff;
  font-size: 21px;
  line-height: 25px;
  font-weight: 600;
  background: #0090ab;
  width: 500px;
  margin-bottom: 10px;
  font-family: 'Montserrat';
  box-sizing: border-box;

}
.product table {
  width: 500px !important;
}
.product tbody tr:first-child {
  background: #f6e6ce;
  border: 1px solid #dccaae;
}
.product .product__description table:last-child tbody tr{
  background-color: #ffffd8;
  color: #cb1f27 !important;
}
.product .product__description table:last-child tbody tr td{
  background-color: #ffffd8;
  color: #cb1f27 !important;
}
.product td {
  padding: 6px 10px;
  font-family: 'Montserrat';
  font-size: 13px;
  font-weight: 400;
  border-color: #dccaae;
  text-align: center;
  color: #6d6b5d;
}
.product td:first-child{
  text-align: left;
}
.table_hd td {
    color: #b0882f;
    font-weight: 700;
}


.product .product__description table:last-child tbody tr td{
  font-size: 18px;
}

.product__price-and-rating {
    margin-top: 0 !important;
}

.sf-tabs__content p {
    font-family: 'Montserrat';
}

@media only screen and (min-device-width: 992px) and (max-device-width: 1080px) {
}
@media only screen and (min-device-width: 601px) and (max-device-width: 991px) {
}
@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {

  .product {
    padding-top:20px;
    width: 100%;
    float: left;
  }
  .product .loading--product-gallery {
    height: auto !important;
    width: 100%;
  }
  .product .sf-gallery__thumbs button {
    height: 80px !important;
    max-width: 80px !important;
  }
  .product .sf-gallery__thumbs button img {
    width: 100%;
    object-fit: contain;
  }
  div#tabs {
    float: left;
    width: 100%;
    margin-top: 0px;
    border-bottom:0px;
  }
  .product .product__info {
    padding-left: 0px !important;
    width: 100% !important;
    max-width: 100% !important;
    margin-top: 30px !important;
  }
  .product .product__info .product__header {
    margin: 0px;
    display: block;
  }
  .product__drag-icon {
    display: none !important;
  }
  .product h3.sf-heading__title.h3 {
    font-size: 24px;
    line-height: 26px;
  }
  .product .product__price-and-rating {
    margin-left: 0px !important;
    margin-top:20px !important;
  }
  .product__rating {
    justify-content: flex-start !important;
    margin-top: 30px !important;
  }
  .sf-add-to-cart__select-quantity button.sf-quantity-selector__button {
    font-size: 21px;
    padding: 0 6px;
  }
  .sf-add-to-cart.product__add-to-cart {
    margin-bottom: 20px !important;
  }
  .product__description.desktop-only{
    display: block !important;
  }
  .product__description  img {
    width: 100%;
    height: auto;
  }

  .pt_col {
    width: 100%;
  }
  .pt_col p {
    margin-top: 2px;
  }
  .sf-tabs__content__tab {
    padding-top: 5px;
    padding-left: 0;
  }
  .sf-tabs__tab .sf-tabs__title {
    border-bottom: 1px solid #3333331f;
    padding-left: 0;
    padding-right: 2px;
  }
  .sf-tabs__title.is-active {
    border-top:0px solid;
  }

  span.sf-product-card__title {
    font-size: 13px;
    line-height: 20px;
    margin-bottom: 5px;
  }
  span.sf-price__regular {
    font-size: 18px;
    margin-bottom: 6px;
  }
  .product__description h4 {
    width:100%;
    padding: 5px 10px;
    font-size: 14px;
  }
  .product table {
    width: 100% !important;
  }
  .product .product__description table:last-child tbody tr td {
    font-size: 15px;
  }
  .product span.sf-price__regular {
    font-size: 22px;
    line-height: 22px;
  }
}

</style>
<style lang="scss" scoped>
@import '../styles.scss';

.product {
  &__select-size {
    margin: 0 var(--spacer-sm);
    @include for-desktop {
      margin: 0;
    }
  }

  &__colors {
    @include font(
        --product-color-font,
        var(--font-weight--normal),
        var(--font-size--lg),
        1.6,
        var(--font-family--secondary)
    );
    display: flex;
    align-items: center;
    margin-top: var(--spacer-xl);

    @include for-mobile {
      margin-left: var(--spacer-sm);
    }
  }

  &__color-label {
    margin: 0 var(--spacer-lg) 0 0;
  }

  &__color {
    margin: 0 var(--spacer-2xs);
  }
}
</style>
