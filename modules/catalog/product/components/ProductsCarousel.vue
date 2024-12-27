<!-- <template>
  <SfSection
    :title-heading="title"
    class="section related_prd_slider"
  >
    <SfLoader
      :class="{ loading }"
      :loading="loading"
    >
      <SfCarousel
        data-cy="related-products-carousel"
        :settings="{ peek: 0, breakpoints: { 1026: { peek: 0, perView:1 }, 1024: { peek: 0, perView:3 }, 600: { peek: 0, perView:2 } } }"
        class="carousel"
      >
        <SfCarouselItem
          v-for="(product, i) in mappedProducts"
          :key="i"
          class="carousel__item"
        >
          <SfProductCard
            image-tag="nuxt-img"
            :title="productGetters.getName(product)"
            :image-width="imageSizes.productCard.width"
            :image-height="imageSizes.productCard.height"
            :image="
              getMagentoImage(productGetters.getProductThumbnailImage(product))
            "
            :nuxt-img-config="{
              fit: 'cover',
            }"
            :regular-price="$fc(productGetters.getPrice(product).regular)"
            :special-price="
              productGetters.getPrice(product).special &&
                $fc(productGetters.getPrice(product).special)
            "
            :link="localePath(getProductPath(product))"
            :max-rating="5"
            :score-rating="productGetters.getAverageRating(product)"
            :reviews-count="productGetters.getTotalReviews(product)"
            :is-in-wishlist="isInWishlist({ product })"
            :is-added-to-cart="isInCart(product)"
            :wishlist-icon="isAuthenticated ? 'heart' : ''"
            :is-in-wishlist-icon="isAuthenticated ? 'heart_fill' : ''"
            @click:wishlist="addItemToWishlist(product)"
            @click:add-to-cart="addItemToCart({ product, quantity: 1 })"
          />
        </SfCarouselItem>
        <template #prev="prevArrow">
          <SfButton
            aria-label="previous"
            class="sf-arrow"
            @click="prevArrow.go('prev')"
          >
            <SvgImage
              icon="arrow_left"
              width="24"
              height="24"
            />
          </SfButton>
        </template>
        <template #next="nextArrow">
          <SfButton
            aria-label="next"
            class="sf-arrow"
            @click="nextArrow.go('next')"
          >
            <SvgImage
              icon="arrow_right"
              width="24"
              height="24"
            />
          </SfButton>
        </template>
      </SfCarousel>
    </SfLoader>
  </SfSection>
</template>

<script lang="ts">
import {
  SfCarousel,
  SfProductCard,
  SfSection,
  SfLoader,
  SfButton,
} from '@storefront-ui/vue';

import { computed, defineComponent, PropType } from '@nuxtjs/composition-api';
import productGetters from '~/modules/catalog/product/getters/productGetters';
import { useAddToCart } from '~/helpers/cart/addToCart';
import { useImage, useProduct } from '~/composables';
import useWishlist from '~/modules/wishlist/composables/useWishlist';
import { useUser } from '~/modules/customer/composables/useUser';
import SvgImage from '~/components/General/SvgImage.vue';
import type { Product } from '~/modules/catalog/product/types';

export default defineComponent({
  name: 'ProductsCarousel',
  components: {
    SfCarousel,
    SfProductCard,
    SfSection,
    SfLoader,
    SfButton,
    SvgImage,
  },
  props: {
    title: {
      type: String,
      required: false,
      default: '',
    },
    products: {
      type: Array as PropType<Product[]>,
      required: false,
      default: () => [],
    },
    loading: Boolean,
  },
  setup(props) {
    const { isAuthenticated } = useUser();
    const { isInWishlist, addOrRemoveItem } = useWishlist();
    const { addItemToCart, isInCart } = useAddToCart();
    const { getProductPath } = useProduct();

    const mappedProducts = computed(() => props.products.map((product) => ({
      ...product,
      isInWishlist: isInWishlist({ product }),
    })));

    const addItemToWishlist = async (product) => {
      await addOrRemoveItem({ product });
    };

    const { getMagentoImage, imageSizes } = useImage();

    return {
      addItemToCart,
      addItemToWishlist,
      isAuthenticated,
      isInCart,
      isInWishlist,
      mappedProducts,
      productGetters,
      getMagentoImage,
      imageSizes,
      getProductPath,
    };
  },
});
</script>

<style lang="scss" scoped>

.section {
  margin-top: var(--spacer-base);
}
.sf-product-card__image img {
    width: 100%;
  }

.carousel {
  margin: 0 calc(-1 * var(--spacer-sm)) 0 0;
  @include for-desktop {
    margin: 0;
  }

  &__item {
    margin: 1.9375rem 0 2.4375rem 0;
  }

  .sf-arrow {
    --button-color: var(--c-dark);

    &:hover {
      --button-color: var(--c-light);
    }
  }
}
</style> -->


<template>
  <SfSection
    :title-heading="title"
    class="section related_prd_slider"
  >
    <SfLoader
      :class="{ loading }"
      :loading="loading"
    >
      <div class="products-list">
        <SfProductCard
          v-for="(product, i) in mappedProducts"
          :key="i"
          image-tag="nuxt-img"
          :title="productGetters.getName(product)"
          :image-width="imageSizes.productCard.width"
          :image-height="imageSizes.productCard.height"
          :image="getMagentoImage(productGetters.getProductThumbnailImage(product))"
          :nuxt-img-config="{ fit: 'cover' }"
          :regular-price="$fc(productGetters.getPrice(product).regular)"
          :special-price="productGetters.getPrice(product).special && $fc(productGetters.getPrice(product).special)"
          :link="localePath(getProductPath(product))"
          :max-rating="5"
          :score-rating="productGetters.getAverageRating(product)"
          :reviews-count="productGetters.getTotalReviews(product)"
          :is-in-wishlist="isInWishlist({ product })"
          :is-added-to-cart="isInCart(product)"
          :wishlist-icon="isAuthenticated ? 'heart' : ''"
          :is-in-wishlist-icon="isAuthenticated ? 'heart_fill' : ''"
          @click:wishlist="addItemToWishlist(product)"
          @click:add-to-cart="addItemToCart({ product, quantity: 1 })"
        />
      </div>
    </SfLoader>
  </SfSection>
</template>
<script lang="ts">
import {
  SfProductCard,
  SfSection,
  SfLoader,
} from '@storefront-ui/vue';
import { computed, defineComponent, PropType } from '@nuxtjs/composition-api';
import productGetters from '~/modules/catalog/product/getters/productGetters';
import { useAddToCart } from '~/helpers/cart/addToCart';
import { useImage, useProduct } from '~/composables';
import useWishlist from '~/modules/wishlist/composables/useWishlist';
import { useUser } from '~/modules/customer/composables/useUser';
import type { Product } from '~/modules/catalog/product/types';
export default defineComponent({
  name: 'ProductsCarousel', // You might want to rename this since it's no longer a carousel
  components: {
    SfProductCard,
    SfSection,
    SfLoader,
  },
  props: {
    title: {
      type: String,
      required: false,
      default: '',
    },
    products: {
      type: Array as PropType<Product[]>,
      required: false,
      default: () => [],
    },
    loading: Boolean,
  },
  setup(props) {
    const { isAuthenticated } = useUser();
    const { isInWishlist, addOrRemoveItem } = useWishlist();
    const { addItemToCart, isInCart } = useAddToCart();
    const { getProductPath } = useProduct();
    const mappedProducts = computed(() => props.products.map((product) => ({
      // @ts-ignore
      ...product,
      isInWishlist: isInWishlist({ product }),
    })));
    const addItemToWishlist = async (product) => {
      await addOrRemoveItem({ product });
    };
    const { getMagentoImage, imageSizes } = useImage();
    return {
      addItemToCart,
      addItemToWishlist,
      isAuthenticated,
      isInCart,
      isInWishlist,
      mappedProducts,
      productGetters,
      getMagentoImage,
      imageSizes,
      getProductPath,
    };
  },
});
</script>
<style lang="scss" scoped>
.section {
  margin-top: var(--spacer-base);
}
.products-list {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacer-md);
}
.products-list .sf-product-card {
  width: calc(33.33% - var(--spacer-md)); /* Adjust based on how many products per row */
}
@media (max-width: 1024px) {
  .products-list .sf-product-card {
    width: calc(50% - var(--spacer-md));
  }
}
@media (max-width: 768px) {
  .products-list .sf-product-card {
    width: 100%;
  }
}
</style>

<style>
.related_prd_slider button.sf-arrow.sf-button {
  background: transparent;
  border-radius: 50px;
  border: 1px solid #a17b20;
}
span.svg-image {
    color: #a17b20;
    width: 18px;
  }

  .related_prd_slider .products-list {
    gap: 25px !important;
    padding: 20px 0 70px 0;
  }
  .related_prd_slider span.sf-product-card__title {
    font-size: 14px;
    line-height: 23px;
  }

@media only screen and (min-device-width: 992px) and (max-device-width: 1080px) {
}
@media only screen and (min-device-width: 601px) and (max-device-width: 991px) {
}
@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  .related_prd_slider .sf-carousel__controls {
    bottom: 0;
    top: auto;
    display: flex;
    z-index: 1;
    gap: 11px;
    justify-content: center;
  }
  span.svg-image {
    color: #a17b20;
    width: 18px;
  }
  
}
</style>
