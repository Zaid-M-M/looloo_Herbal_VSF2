<template>
  <SfSidebar
    :title="currentCategory && currentCategory.name || $t('Menu')"
    visible
    class="mobile-menu-sidebar sf-sidebar--left"
    @close="toggleMobileMenu"
  >
    <SfList class="mobile-menu-sidebar__list">
      <!-- <template v-if="currentCategory">
        <SfMenuItem
          class="mobile-menu-sidebar__item"
          :label="$i18n.t('Go back')"
          @click="onGoCategoryUp()"
        >
          <template #mobile-nav-icon>
            <div v-show="false" />
          </template>
        </SfMenuItem>

        <SfMenuItem
          class="mobile-menu-sidebar__item"
          :label="$i18n.t('AllProductsFromCategory', { categoryName: currentCategory.name })"
          @click="navigate(currentCategory)"
        />
      </template> -->

      <!-------------------------------------------------------------------------------------------------- Static menu items -->


      <!-- Oral Care Menu -->
       <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl" @click="toggleMenu2">
        <template #label><p @click="navigateTo('/default/oral-care.html')">Oral Care</p></template>
        <template #mobile-nav-icon>
          <span class="accord_icon">{{ isMenu2Expanded ? '-' : '+' }}</span>
        </template>
      </SfMenuItem>
      <transition name="collapse">
        <SfList v-if="isMenu2Expanded" class="mobile-menu-sidebar__list">
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Herbal Dental Gel Laung (Clove) 100g')"
            @click="navigateTo('/default/looloo-herbal-dental-gel-laung-clove-100g.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Herbal Dental Gel Neem 100g')"
            @click="navigateTo('/default/looloo-herbal-dental-gel-neem-100g.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Herbal Dental Gel MisKal with Peelu Bark & Kalonji 100g')"
            @click="navigateTo('/default/looloo-herbal-dental-gel-miskal-with-peelu-bark-kalonji-100g.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Herbal Dental Gel AquaMint 100g')"
            @click="navigateTo('/default/looloo-herbal-dental-gel-aquamint-100g.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Herbal Dental Gel Charcoal 100g')"
            @click="navigateTo('default/looloo-herbal-dental-gel-charcoal-100g.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Herbal Medicated Tooth Powder Laung (Clove) 50g')"
            @click="navigateTo('/default/looloo-herbal-medicated-tooth-powder-laung-clove-50g.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Herbal Medicated Tooth Powder Neem 50g')"
            @click="navigateTo('/default/looloo-herbal-medicated-tooth-powder-neem-50g.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Herbal Medicated Toothpowder MisKal 50g')"
            @click="navigateTo('/default/looloo-herbal-medicated-toothpowder-miskal-50g.html')"
          />
        </SfList>
      </transition>

      <!-- Hair Care Menu -->
      <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl" @click="toggleMenu3">
        <template #label><p @click="navigateTo('/default/oral-care.html')">Hair Care</p></template>
        <template #mobile-nav-icon>
          <span class="accord_icon">{{ isMenu3Expanded ? '-' : '+' }}</span>
        </template>
      </SfMenuItem>
      <transition name="collapse">
        <SfList v-if="isMenu3Expanded" class="mobile-menu-sidebar__list">
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Mumtaz Amla Hair Oil 120ml')"
            @click="navigateTo('/default/looloo-mumtaz-amla-hair-oil-120ml.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Roshan-e-Zulf Herbal Hair Oil 120ml')"
            @click="navigateTo('/default/looloo-roshan-e-zulf-herbal-hair-oil-120ml.html')"
          />
        </SfList>
      </transition>


      <!-- Joint Relief Menu -->
      <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl" @click="toggleMenu4">
        <template #label><p @click="navigateTo('/default/joint-relief.html')">Joint Relief</p></template>
        <template #mobile-nav-icon>
          <span class="accord_icon">{{ isMenu4Expanded ? '-' : '+' }}</span>
        </template>
      </SfMenuItem>
      <transition name="collapse">
        <SfList v-if="isMenu4Expanded" class="mobile-menu-sidebar__list">
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Oleo Rheuma Herbal Liniment Gel 40g')"
            @click="navigateTo('/default/looloo-oleo-rheuma-herbal-liniment-gel-40g.html')"
          />
          
          <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl_1" @click="toggleMenu4_1">
            <template #label><p @click="navigateTo('/default/joint-relief/looloo-oleo-rheuma-herbal-liniment-with-kalonji.html')">LooLoo Oleo Rheuma Herbal Liniment with Kalonji</p></template>
            <template #mobile-nav-icon>
              <span class="accord_icon">{{ isMenu4_1Expanded ? '-' : '+' }}</span>
            </template>
          </SfMenuItem>

          <transition name="collapse">
            <SfList v-if="isMenu4_1Expanded" class="mobile-menu-sidebar__list collapse-content">
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Rheuma Herbal Liniment with Kalonji 200ml')"
                @click="navigateTo('/default/looloo-oleo-rheuma-herbal-liniment-with-kalonji-200ml.html')"
              />
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Rheuma Herbal Liniment with Kalonji 100ml')"
                @click="navigateTo('/default/looloo-oleo-rheuma-herbal-liniment-with-kalonji-100ml.html')"
              />
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Rheuma Herbal Liniment with Kalonji 50ml')"
                @click="navigateTo('/default/looloo-oleo-rheuma-herbal-liniment-with-kalonji-50ml.html')"
              />
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Rheuma Herbal Liniment with Kalonji 15ml')"
                @click="navigateTo('/default/looloo-oleo-rheuma-herbal-liniment-with-kalonji-15ml.html')"
              />
            </SfList>
          </transition>


        </SfList>
      </transition>

      <!-- Massage Oil Menu -->
      <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl" @click="toggleMenu5">
        <template #label><p @click="navigateTo('/default/massage-oil.html')">Massage Oil</p></template>
        <template #mobile-nav-icon>
          <span class="accord_icon">{{ isMenu5Expanded ? '-' : '+' }}</span>
        </template>
      </SfMenuItem>
      <transition name="collapse">
        <SfList v-if="isMenu5Expanded" class="mobile-menu-sidebar__list">
          
          <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl_1" @click="toggleMenu5_1">
            <template #label><p @click="navigateTo('/default/massage-oil/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric.html')">LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric</p></template>
            <template #mobile-nav-icon>
              <span class="accord_icon">{{ isMenu5_1Expanded ? '-' : '+' }}</span>
            </template>
          </SfMenuItem>
          <transition name="collapse">
            <SfList v-if="isMenu5_1Expanded" class="mobile-menu-sidebar__list collapse-content">
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric 200ml')"
                @click="navigateTo('/default/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric-200ml.html')"
              />
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric 100ml')"
                @click="navigateTo('/default/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric-100ml.html')"
              />
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric 50ml')"
                @click="navigateTo('/default/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric-50ml.html')"
              />
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric 25ml')"
                @click="navigateTo('/default/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric-25ml.html')"
              />
            </SfList>
          </transition>

          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Nanha Farishta Baby Massage Oil 120ml')"
            @click="navigateTo('/default/looloo-nanha-farishta-baby-massage-oil-120ml.html')"
          />


        </SfList>
      </transition>

      <!-- Immunity Booster Menu -->
      <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl" @click="toggleMenu6">
        <template #label><p @click="navigateTo('/default/immunity-booster.html')">Immunity Booster</p></template>
        <template #mobile-nav-icon>
          <span class="accord_icon">{{ isMenu6Expanded ? '-' : '+' }}</span>
        </template>
      </SfMenuItem>
      <transition name="collapse">
        <SfList v-if="isMenu6Expanded" class="mobile-menu-sidebar__list">
          
          <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl_1" @click="toggleMenu6_1">
            <template #label><p @click="navigateTo('/default/immunity-booster/looloo-black-gold-kalonji-oil.html')">LooLoo Black Gold Kalonji Oil</p></template>
            <template #mobile-nav-icon>
              <span class="accord_icon">{{ isMenu6_1Expanded ? '-' : '+' }}</span>
            </template>
          </SfMenuItem>
          <transition name="collapse">
            <SfList v-if="isMenu6_1Expanded" class="mobile-menu-sidebar__list collapse-content">
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Black Gold Kalonji Oil 100ml')"
                @click="navigateTo('/default/looloo-black-gold-kalonji-oil-100ml.html')"
              />
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Black Gold Kalonji Oil 50ml')"
                @click="navigateTo('/default/looloo-black-gold-kalonji-oil-50ml.html')"
              />
            </SfList>
          </transition>

          <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl_1" @click="toggleMenu6_2">
            <template #label><p @click="navigateTo('/default/immunity-booster/looloo-oleo-shifa-medicated-oil.html')">LooLoo Oleo Shifa Medicated Oil</p></template>
            <template #mobile-nav-icon>
              <span class="accord_icon">{{ isMenu6_2Expanded ? '-' : '+' }}</span>
            </template>
          </SfMenuItem>
          <transition name="collapse">
            <SfList v-if="isMenu6_2Expanded" class="mobile-menu-sidebar__list collapse-content">
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Shifa Medicated Oil with Kalonji')"
                @click="navigateTo('/default/looloo-oleo-shifa-medicated-oil-with-kalonji.html')"
              />
              <SfMenuItem
                class="mobile-menu-sidebar__item mob_menu_lbl_2"
                :label="$i18n.t('LooLoo Oleo Shifa Medicated Oil with Kalonji Pack of 6')"
                @click="navigateTo('/default/looloo-oleo-shifa-medicated-oil-with-kalonji-pack-of-6.html')"
              />
            </SfList>
          </transition>

        </SfList>
      </transition>

       <!-- Cold & Headache Menu -->
       <SfMenuItem class="mobile-menu-sidebar__item mob_menu_lbl" @click="toggleMenu7">
        <template #label><p @click="navigateTo('/default/cold-headache.html')">Cold & Headache</p></template>
        <template #mobile-nav-icon>
          <span class="accord_icon">{{ isMenu7Expanded ? '-' : '+' }}</span>
        </template>
      </SfMenuItem>
      <transition name="collapse">
        <SfList v-if="isMenu7Expanded" class="mobile-menu-sidebar__list">
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Oleo Cold Shield Roll-On Oil with Kalonji')"
            @click="navigateTo('/default/looloo-oleo-cold-shield-roll-on-oil-with-kalonji.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('Cold Relief Offer Pack of 3')"
            @click="navigateTo('/default/cold-relief-offer-pack-of-3.html')"
          />
          <SfMenuItem
            class="mobile-menu-sidebar__item mob_menu_lbl_1"
            :label="$i18n.t('LooLoo Oleo Cold Shield Roll-On Oil with Kalonji Pack of 8')"
            @click="navigateTo('/default/looloo-oleo-cold-shield-roll-on-oil-with-kalonji-pack-of-8.html')"
          />
        </SfList>
      </transition>
      <!-- <SfMenuItem class="mobile-menu-sidebar__item" :label="$i18n.t('Menu3')" />
      <SfMenuItem class="mobile-menu-sidebar__item" :label="$i18n.t('Menu4')" /> -->
      
      <!-- <SfMenuItem
        v-for="category in itemsIncludedInMenu"
        :key="category.uid"
        :label="category.name"
        class="mobile-menu-sidebar__item"
        @click="category.children && category.children.length > 0 ? onGoCategoryDown(category) : navigate(category)"
      /> -->
    </SfList>
  </SfSidebar>
</template>
<script lang="ts">
import {
  SfSidebar, SfList, SfMenuItem,
} from '@storefront-ui/vue';
import {
  defineComponent, useRouter, useContext, computed,ref,
} from '@nuxtjs/composition-api';
import { useUiHelpers, useUiState } from '~/composables';
import { useTraverseCategory } from '~/modules/catalog/category/helpers/useTraverseCategory';
import { CategoryTree } from '~/modules/GraphQL/types';
import { useMobileCategoryTree } from './logic';

export default defineComponent({
  components: {
    SfSidebar,
    SfList,
    SfMenuItem,
  },
  setup() {
    const { isMobileMenuOpen, toggleMobileMenu } = useUiState();
    const { getCatLink } = useUiHelpers();
    const router = useRouter();
    const app = useContext();

    const { categoryAncestors: initialHistory, categoryTree } = useTraverseCategory();

    const navigate = (category: CategoryTree) => {
      toggleMobileMenu();
      const path = app.localePath(getCatLink(category) as string);
      router.push(path);
    };

    // A category with no child categories can't be entered into - it can only navigated to
    const initialHistoryWithSnippedSubcategoryLessTail = initialHistory.value.at(-1)?.children?.length
      ? initialHistory.value
      : initialHistory.value.slice(0, -1);

    const {
      current: currentCategory, history, currentItems, onGoCategoryUp, onGoCategoryDown,
    } = useMobileCategoryTree(initialHistoryWithSnippedSubcategoryLessTail);

    const itemsIncludedInMenu = computed(() => {
      const topLevelItems = categoryTree.value.children;
      const maybeCurrentCategoryItems = currentItems.value || topLevelItems;

      return maybeCurrentCategoryItems.filter((item) => item.include_in_menu);
    });

    const isMenu2Expanded = ref(false);

    const isMenu3Expanded = ref(false);

    const isMenu4Expanded = ref(false);
    const isMenu4_1Expanded = ref(false);

    const isMenu5Expanded = ref(false);
    const isMenu5_1Expanded = ref(false);

    const isMenu6Expanded = ref(false);
    const isMenu6_1Expanded = ref(false);
    const isMenu6_2Expanded = ref(false);

    const isMenu7Expanded = ref(false);

    const toggleMenu2 = () => {
      isMenu2Expanded.value = !isMenu2Expanded.value;
      if (isMenu2Expanded.value) isMenu3Expanded.value = false;
      if (isMenu2Expanded.value) isMenu4Expanded.value = false;
      if (isMenu2Expanded.value) isMenu5Expanded.value = false;
      if (isMenu2Expanded.value) isMenu6Expanded.value = false;
      if (isMenu2Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu3 = () => {
      isMenu3Expanded.value = !isMenu3Expanded.value;
      if (isMenu3Expanded.value) isMenu2Expanded.value = false;
      if (isMenu3Expanded.value) isMenu4Expanded.value = false;
      if (isMenu3Expanded.value) isMenu5Expanded.value = false;
      if (isMenu3Expanded.value) isMenu6Expanded.value = false;
      if (isMenu3Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu4 = () => {
      isMenu4Expanded.value = !isMenu4Expanded.value;
      if (isMenu4Expanded.value) isMenu2Expanded.value = false;
      if (isMenu4Expanded.value) isMenu3Expanded.value = false;
      if (isMenu4Expanded.value) isMenu5Expanded.value = false;
      if (isMenu4Expanded.value) isMenu6Expanded.value = false;
      if (isMenu4Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu4_1 = () => {
      isMenu4_1Expanded.value = !isMenu4_1Expanded.value;
      if (isMenu4_1Expanded.value) isMenu2Expanded.value = false;
      if (isMenu4_1Expanded.value) isMenu3Expanded.value = false;
      if (isMenu4_1Expanded.value) isMenu5Expanded.value = false;
      if (isMenu4_1Expanded.value) isMenu6Expanded.value = false;
      if (isMenu4_1Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu5 = () => {
      isMenu5Expanded.value = !isMenu5Expanded.value;
      if (isMenu5Expanded.value) isMenu2Expanded.value = false;
      if (isMenu5Expanded.value) isMenu3Expanded.value = false;
      if (isMenu5Expanded.value) isMenu4Expanded.value = false;
      if (isMenu5Expanded.value) isMenu6Expanded.value = false;
      if (isMenu5Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu5_1 = () => {
      isMenu5_1Expanded.value = !isMenu5_1Expanded.value;
      if (isMenu5_1Expanded.value) isMenu2Expanded.value = false;
      if (isMenu5_1Expanded.value) isMenu3Expanded.value = false;
      if (isMenu5_1Expanded.value) isMenu4Expanded.value = false;
      if (isMenu5_1Expanded.value) isMenu6Expanded.value = false;
      if (isMenu5_1Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu6 = () => {
      isMenu6Expanded.value = !isMenu6Expanded.value;
      if (isMenu6Expanded.value) isMenu2Expanded.value = false;
      if (isMenu6Expanded.value) isMenu3Expanded.value = false;
      if (isMenu6Expanded.value) isMenu4Expanded.value = false;
      if (isMenu6Expanded.value) isMenu5Expanded.value = false;
      if (isMenu6Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu6_1 = () => {
      isMenu6_1Expanded.value = !isMenu6_1Expanded.value;
      if (isMenu6_1Expanded.value) isMenu2Expanded.value = false;
      if (isMenu6_1Expanded.value) isMenu3Expanded.value = false;
      if (isMenu6_1Expanded.value) isMenu4Expanded.value = false;
      if (isMenu6_1Expanded.value) isMenu5Expanded.value = false;
      if (isMenu6_1Expanded.value) isMenu6_2Expanded.value = false;
      if (isMenu6_1Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu6_2 = () => {
      isMenu6_2Expanded.value = !isMenu6_2Expanded.value;
      if (isMenu6_2Expanded.value) isMenu2Expanded.value = false;
      if (isMenu6_2Expanded.value) isMenu3Expanded.value = false;
      if (isMenu6_2Expanded.value) isMenu4Expanded.value = false;
      if (isMenu6_2Expanded.value) isMenu5Expanded.value = false;
      if (isMenu6_2Expanded.value) isMenu6_1Expanded.value = false;
      if (isMenu6_2Expanded.value) isMenu7Expanded.value = false;
    };

    const toggleMenu7 = () => {
      isMenu7Expanded.value = !isMenu7Expanded.value;
      if (isMenu7Expanded.value) isMenu2Expanded.value = false;
      if (isMenu7Expanded.value) isMenu3Expanded.value = false;
      if (isMenu7Expanded.value) isMenu4Expanded.value = false;
      if (isMenu7Expanded.value) isMenu5Expanded.value = false;
      if (isMenu7Expanded.value) isMenu6Expanded.value = false;
    };


    // Function to navigate to different pages
    const navigateTo = (path: string) => {
      toggleMobileMenu();
      router.push(path);
    };

    return {
      currentCategory,
      onGoCategoryUp,
      onGoCategoryDown,
      history,
      navigate,
      isMobileMenuOpen,
      toggleMobileMenu,
      itemsIncludedInMenu,
      navigateTo,

      isMenu2Expanded,
      toggleMenu2,

      isMenu3Expanded, 
      toggleMenu3,

      isMenu4Expanded, 
      toggleMenu4,

      isMenu4_1Expanded, 
      toggleMenu4_1,

      isMenu5Expanded, 
      toggleMenu5,

      isMenu5_1Expanded, 
      toggleMenu5_1,

      isMenu6Expanded, 
      toggleMenu6,

      isMenu6_1Expanded, 
      toggleMenu6_1,

      isMenu6_2Expanded, 
      toggleMenu6_2,

      isMenu7Expanded, 
      toggleMenu7,
    };
  },
});
</script>

<style>

.mobile-menu-sidebar .sf-bar.smartphone-only {
    background: #05923F;
    color: #fff;
    font-family: 'Montserrat';
    font-size: 20px;
}
.mobile-menu-sidebar .sf-bar.smartphone-only .sf-bar__icon span{
  fill: #fff;
}
.accord_icon {
    font-size: 26px;
    font-family: 'Oxygen';
}

.mob_menu_lbl {
    font-family: 'Montserrat';
    font-size: 14px;
    padding: 0 0 !important;
    height: 45px;
    text-transform: uppercase;
    font-weight: 600;
    color: #978d4b;
    text-align: left;
}
.mob_menu_lbl_1 {
  font-family: "Montserrat";
  font-size: 12px;
  padding: 0 0 !important;
  height: auto;
  text-transform: uppercase;
  font-weight: 400;
  color: #978d4b !important;
  padding-left: 20px !important;
  padding-right: 0px !important;
  border: none !important;
  margin: 13px 0px;
  text-align: left;
}
.mob_menu_lbl_1 span {
  color: #978d4b !important;
}
.mob_menu_lbl_2 {
  font-family: "Montserrat";
  font-size: 12px;
  padding: 0 0 !important;
  height: auto;
  text-transform: uppercase;
  font-weight: 400;
  color: #978d4b !important;
  padding-left: 40px !important;
  padding-right: 0px !important;
  border: none !important;
  margin: 13px 0px;
  text-align: left;
}
.mob_menu_lbl_2 span {
  color: #978d4b !important;
}
span.sf-menu-item__mobile-nav-icon.smartphone-only.sf-icon {
    display: none !important;
}
</style>

<style lang="scss" scoped>
.mobile-menu-sidebar {
  --sidebar-z-index: 3;
  --overlay-z-index: 3;

  &__list {
    .mobile-menu-sidebar__item {
      padding: var(--spacer-base) 0;
      --menu-item-font-size: 1.75rem;

      &:not(:first-of-type) {
        border-top: 1px solid var(--c-light);
      }

      &:not(:last-of-type) {
        border-bottom: 1px solid var(--c-light);
      }
    }
  }

  ::v-deep {
    .nuxt-link-active {
      --menu-item-label-color: var(--c-primary);
    }
  }
}

.collapse-enter-active, .collapse-leave-active {
  transition: max-height 0.3s ease, opacity 0.3s ease;
}

.collapse-enter, .collapse-leave-to {
  max-height: 0;
  opacity: 0;
  overflow: hidden;
}

.collapse-enter-to, .collapse-leave {
  max-height: 1000px; /* Set a large value for transition */
  opacity: 1;
}
.go-back {
  display: flex;
  align-items: center;
}
</style>
