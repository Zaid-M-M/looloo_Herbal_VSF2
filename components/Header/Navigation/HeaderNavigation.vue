<template>
  <div
    class="header-navigation"
   @mouseleave="setCurrentCategory(null)"
  >
    <div class="sf-header-navigation-item__item sf-header-navigation-item__item--desktop">
      <!-- <HeaderNavigationItem
        v-for="(category, index) in categoryTree"
        :key="index"
        ref="lvl0CatRefs"
        :data-testid="category.uid"
        :label="category.name"
        :link="localePath(getCatLink(category))"
        tabindex="1"
        aria-haspopup="true"
        class="nav-item"
        :data-index="index"
        :has-children="hasChildren(category)"
        @mouseenter.native.prevent="onMouseEnter(category)"
        @keydown.down.native.prevent="setCurrentCategory(category)"
        @keydown.up.native.prevent="setCurrentCategory(null)"
        @keyup.tab.native.prevent="setFocus($event)"
        @keydown.right.native.prevent="navRight()"
        @keydown.left.native.prevent="navLeft()"
      /> -->

      <!-- Oral Care Menu Start Here-->
       
      <a href="/default/oral-care.html" class="sf-link sf-header-navigation-item__link nav-item custom_menu menu1" 
        @mouseenter="showDropdown"
        @mouseleave="handleMouseLeave"
      > Oral Care 

        <span class="sf-icon color-green-primary size-xxs" style="">
          <svg viewBox="0 0 24 24" preserveAspectRatio="none" class="sf-icon-path">
            <defs class="">
              <linearGradient id="linearGradient-39" x1="0" y1="0" x2="1" y2="0">
                <stop offset="1" stop-color="var(--icon-color)"></stop>
                <stop offset="0" stop-color="var(--icon-color-negative, var(--c-gray-variant))"></stop>
              </linearGradient>
            </defs>
            <path d="M2 8.364L3.6 7l8.4 7.254L20.4 7 22 8.364 12 17z" fill="var(--icon-color)" style="height: 100%;"></path>
          </svg>
        </span> 

        <!-- Oral Care Menu Dropdown Here-->
        <div class="header-navigation__subcategories custom_dropdown menu1_dropdown"  v-if="isDropdownVisible" @mouseenter="showDropdown"
        @mouseleave="hideDropdown">
          <div class="header-navigation__subcategories-inner">


            <div class="header-navigation__subcategory">
              <SfLink class="header-navigation__link1" link="/default/looloo-herbal-dental-gel-laung-clove-100g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5"> LooLoo Herbal Dental Gel Laung (Clove) 100g</h2>
              </SfLink>
              <SfLink class="header-navigation__link1"  link="/default/looloo-herbal-dental-gel-neem-100g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Herbal Dental Gel Neem 100g</h2>
              </SfLink>
              <SfLink class="header-navigation__link1" link="/default/looloo-herbal-dental-gel-miskal-with-peelu-bark-kalonji-100g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Herbal Dental Gel MisKal with Peelu Bark & Kalonji 100g
                </h2>
              </SfLink>
              <SfLink class="header-navigation__link1" link="/default/looloo-herbal-dental-gel-aquamint-100g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Herbal Dental Gel AquaMint 100g</h2>
              </SfLink>
              <SfLink class="header-navigation__link1"  link="/default/looloo-herbal-dental-gel-charcoal-100g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Herbal Dental Gel Charcoal 100g</h2>
              </SfLink>
              <SfLink class="header-navigation__link1" link="/default/looloo-herbal-medicated-tooth-powder-laung-clove-50g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Herbal Medicated Tooth Powder Laung (Clove) 50g</h2>
              </SfLink>
              <SfLink class="header-navigation__link1" link="/default/looloo-herbal-medicated-tooth-powder-neem-50g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Herbal Medicated Tooth Powder Neem 50g</h2>
              </SfLink>
              <SfLink class="header-navigation__link1" link="/default/looloo-herbal-medicated-toothpowder-miskal-50g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Herbal Medicated Toothpowder MisKal 50g</h2>
              </SfLink>
            </div>

          </div>
        </div>
        <!-- Oral Care Dropdown End Here-->

      </a>
       <!-- Oral Care Menu End Here--> 

       <!-- Hair Care Menu Start Here-->
      <a href="/default/hair-care.html" class="sf-link sf-header-navigation-item__link nav-item custom_menu menu2" 
        @mouseenter="showDropdown1"
        @mouseleave="handleMouseLeave1"
      > Hair Care 

        <span class="sf-icon color-green-primary size-xxs" style="">
          <svg viewBox="0 0 24 24" preserveAspectRatio="none" class="sf-icon-path">
            <defs class="">
              <linearGradient id="linearGradient-39" x1="0" y1="0" x2="1" y2="0">
                <stop offset="1" stop-color="var(--icon-color)"></stop>
                <stop offset="0" stop-color="var(--icon-color-negative, var(--c-gray-variant))"></stop>
              </linearGradient>
            </defs>
            <path d="M2 8.364L3.6 7l8.4 7.254L20.4 7 22 8.364 12 17z" fill="var(--icon-color)" style="height: 100%;"></path>
          </svg>
        </span> 

        <!-- Hair Care Menu Dropdown Here-->
        <div class="header-navigation__subcategories custom_dropdown menu2_dropdown"  v-if="isDropdownVisible1" @mouseenter="showDropdown1"
        @mouseleave="hideDropdown1">
          <div class="header-navigation__subcategories-inner">


            <div class="header-navigation__subcategory">
              <SfLink class="header-navigation__link1" link="/default/looloo-mumtaz-amla-hair-oil-120ml.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5"> LooLoo Mumtaz Amla Hair Oil 120ml</h2>
              </SfLink>
              <SfLink class="header-navigation__link1" link="/default/looloo-roshan-e-zulf-herbal-hair-oil-120ml.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Roshan-e-Zulf Herbal Hair Oil 120ml</h2>
              </SfLink>
            </div>

          </div>
        </div>
        <!-- Hair Care Dropdown End Here-->

      </a>
       <!-- Hair Care Menu End Here-->
        
      <!-- Joint Relief Menu Start Here-->
      <a href="/default/joint-relief.html" class="sf-link sf-header-navigation-item__link nav-item custom_menu menu3" 
        @mouseenter="showDropdown2"
        @mouseleave="handleMouseLeave2"
      > Joint Relief

        <span class="sf-icon color-green-primary size-xxs" style="">
          <svg viewBox="0 0 24 24" preserveAspectRatio="none" class="sf-icon-path">
            <defs class="">
              <linearGradient id="linearGradient-39" x1="0" y1="0" x2="1" y2="0">
                <stop offset="1" stop-color="var(--icon-color)"></stop>
                <stop offset="0" stop-color="var(--icon-color-negative, var(--c-gray-variant))"></stop>
              </linearGradient>
            </defs>
            <path d="M2 8.364L3.6 7l8.4 7.254L20.4 7 22 8.364 12 17z" fill="var(--icon-color)" style="height: 100%;"></path>
          </svg>
        </span> 

        <!-- Joint Relief Menu Dropdown Here-->
        <div class="header-navigation__subcategories custom_dropdown menu2_dropdown"  v-if="isDropdownVisible2" @mouseenter="showDropdown2"  @mouseleave="hideDropdown2">
          <div class="header-navigation__subcategories-inner">
            
            <div class="header-navigation__subcategory">
              <SfLink class="header-navigation__link1" link="/default/looloo-oleo-rheuma-herbal-liniment-gel-40g.html">
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5"> LooLoo Oleo Rheuma Herbal Liniment Gel 40g</h2>
              </SfLink>
              <a class="header-navigation__link1" href="/default/joint-relief/looloo-oleo-rheuma-herbal-liniment-with-kalonji.html">
                  <div @mouseenter="showDropdown3_3rdLevel" @mouseleave="hideDropdown3_3rdLevel">
                      <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5 desk_3rd_level_menu">LooLoo Oleo Rheuma Herbal Liniment with Kalonji</h2>
                  </div>
                  <div class="header-navigation__subcategories custom_dropdown menu2_dropdown desk_3rd_level_dropdown"  v-show="isDropdownVisible3_3rdLevel" @mouseenter="showDropdown3_3rdLevel"  @mouseleave="hideDropdown3_3rdLevel">

                    <div class="header-navigation__subcategories-inner">
                      <div class="header-navigation__subcategory">
                        <SfLink class="header-navigation__link1" link="/default/looloo-oleo-rheuma-herbal-liniment-with-kalonji-200ml.html">
                          <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Rheuma Herbal Liniment with Kalonji 200ml</h2>
                        </SfLink>
                        <SfLink class="header-navigation__link1" link="/default/looloo-oleo-rheuma-herbal-liniment-with-kalonji-100ml.html">
                          <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Rheuma Herbal Liniment with Kalonji 100ml</h2>
                        </SfLink>
                        <SfLink class="header-navigation__link1" link="/default/looloo-oleo-rheuma-herbal-liniment-with-kalonji-50ml.html">
                          <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Rheuma Herbal Liniment with Kalonji 50ml</h2>
                        </SfLink>
                        <SfLink class="header-navigation__link1" link="/default/looloo-oleo-rheuma-herbal-liniment-with-kalonji-15ml.html">
                          <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Rheuma Herbal Liniment with Kalonji 15ml</h2>
                        </SfLink>
                      </div>
                    </div>

                  </div>
                </a>
            </div>

          </div>
        </div>
        <!-- Joint Relief Dropdown End Here-->

      </a>
       <!-- Joint Relief Menu End Here-->

      <!-- Massage Oil Menu Start Here-->
      <a href="/default/massage-oil.html" class="sf-link sf-header-navigation-item__link nav-item custom_menu menu4" 
              @mouseenter="showDropdown3"
              @mouseleave="handleMouseLeave3"
            > Massage Oil 

        <span class="sf-icon color-green-primary size-xxs" style="">
          <svg viewBox="0 0 24 24" preserveAspectRatio="none" class="sf-icon-path">
            <defs class="">
              <linearGradient id="linearGradient-39" x1="0" y1="0" x2="1" y2="0">
                <stop offset="1" stop-color="var(--icon-color)"></stop>
                <stop offset="0" stop-color="var(--icon-color-negative, var(--c-gray-variant))"></stop>
              </linearGradient>
            </defs>
            <path d="M2 8.364L3.6 7l8.4 7.254L20.4 7 22 8.364 12 17z" fill="var(--icon-color)" style="height: 100%;"></path>
          </svg>
        </span> 

        <!-- Massage Oil Dropdown Here-->
        <div class="header-navigation__subcategories custom_dropdown menu2_dropdown"  v-if="isDropdownVisible3" @mouseenter="showDropdown3"
        @mouseleave="hideDropdown3">
          <div class="header-navigation__subcategories-inner">


            <div class="header-navigation__subcategory">
              
                <a class="header-navigation__link1" href="/default/massage-oil/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric.html">
                  <div @mouseenter="showDropdown4_3rdLevel" @mouseleave="hideDropdown4_3rdLevel">
                      <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5 desk_3rd_level_menu">LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric</h2>
                  </div>
                  <div class="header-navigation__subcategories custom_dropdown menu2_dropdown desk_3rd_level_dropdown top_3rd_dp"  v-show="isDropdownVisible4_3rdLevel" @mouseenter="showDropdown4_3rdLevel"  @mouseleave="hideDropdown4_3rdLevel">

                    <div class="header-navigation__subcategories-inner">
                      <div class="header-navigation__subcategory">
                        <SfLink class="header-navigation__link1" link="/default/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric-200ml.html">
                          <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric 200ml</h2>
                        </SfLink>
                        <SfLink class="header-navigation__link1" link="/default/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric-100ml.html">
                          <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric 100ml</h2>
                        </SfLink>
                        <SfLink class="header-navigation__link1" link="/default/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric-50ml.html">
                          <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric 50ml</h2>
                        </SfLink>
                        <SfLink class="header-navigation__link1" link="/default/looloo-oleo-hayat-herbal-massage-oil-with-kalonji-turmeric-25ml.html">
                          <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Hayat Herbal Massage Oil with Kalonji & Turmeric 25ml</h2>
                        </SfLink>
                      </div>
                    </div>

                  </div>
                </a>
                <SfLink class="header-navigation__link1" link="/default/looloo-nanha-farishta-baby-massage-oil-120ml.html">
                  <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Nanha Farishta Baby Massage Oil 120m</h2>
                </SfLink>
            </div>

          </div>
        </div>
        <!-- Massage Oil Dropdown End Here-->

      </a>
       <!-- Massage Oil Menu End Here-->

      <!-- Immunity Booster Menu Start Here-->
      <a href="/default/immunity-booster.html" class="sf-link sf-header-navigation-item__link nav-item custom_menu menu5" 
              @mouseenter="showDropdown4"
              @mouseleave="handleMouseLeave4"
            > Immunity Booster

        <span class="sf-icon color-green-primary size-xxs" style="">
          <svg viewBox="0 0 24 24" preserveAspectRatio="none" class="sf-icon-path">
            <defs class="">
              <linearGradient id="linearGradient-39" x1="0" y1="0" x2="1" y2="0">
                <stop offset="1" stop-color="var(--icon-color)"></stop>
                <stop offset="0" stop-color="var(--icon-color-negative, var(--c-gray-variant))"></stop>
              </linearGradient>
            </defs>
            <path d="M2 8.364L3.6 7l8.4 7.254L20.4 7 22 8.364 12 17z" fill="var(--icon-color)" style="height: 100%;"></path>
          </svg>
        </span> 

        <!-- Immunity Booster Dropdown Here-->
        <div class="header-navigation__subcategories custom_dropdown menu2_dropdown"  v-if="isDropdownVisible4" @mouseenter="showDropdown4"
        @mouseleave="hideDropdown4">
          <div class="header-navigation__subcategories-inner">


            <div class="header-navigation__subcategory">

              <a class="header-navigation__link1" href="/default/immunity-booster/looloo-black-gold-kalonji-oil.html">
                <div @mouseenter="showDropdown5_3rdLevel" @mouseleave="hideDropdown5_3rdLevel">
                    <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5 desk_3rd_level_menu">LooLoo Black Gold Kalonji Oil</h2>
                </div>
                <div class="header-navigation__subcategories custom_dropdown menu2_dropdown desk_3rd_level_dropdown top_3rd_dp"  v-show="isDropdownVisible5_3rdLevel" @mouseenter="showDropdown5_3rdLevel"  @mouseleave="hideDropdown5_3rdLevel">

                  <div class="header-navigation__subcategories-inner">
                    <div class="header-navigation__subcategory">
                      <SfLink class="header-navigation__link1" link="/default/looloo-black-gold-kalonji-oil-100ml.html">
                        <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Black Gold Kalonji Oil 100ml</h2>
                      </SfLink>
                      <SfLink class="header-navigation__link1" link="/default/looloo-black-gold-kalonji-oil-50ml.html">
                        <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Black Gold Kalonji Oil 50ml</h2>
                      </SfLink>
                    </div>
                  </div>

                </div>
              </a>
              <a class="header-navigation__link1" href="/default/immunity-booster/looloo-oleo-shifa-medicated-oil.html">
                <div @mouseenter="showDropdown5_1_3rdLevel" @mouseleave="hideDropdown5_1_3rdLevel">
                    <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5 desk_3rd_level_menu">LooLoo Oleo Shifa Medicated Oil</h2>
                </div>
                <div class="header-navigation__subcategories custom_dropdown menu2_dropdown desk_3rd_level_dropdown"  v-show="isDropdownVisible5_1_3rdLevel" @mouseenter="showDropdown5_1_3rdLevel"  @mouseleave="hideDropdown5_1_3rdLevel">

                  <div class="header-navigation__subcategories-inner">
                    <div class="header-navigation__subcategory">
                      <SfLink class="header-navigation__link1" link="/default/looloo-oleo-shifa-medicated-oil-with-kalonji.html">
                        <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Shifa Medicated Oil with Kalonji</h2>
                      </SfLink>
                      <SfLink class="header-navigation__link1" link="/default/looloo-oleo-shifa-medicated-oil-with-kalonji-pack-of-6.html">
                        <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Shifa Medicated Oil with Kalonji Pack of 6</h2>
                      </SfLink>
                    </div>
                  </div>

                </div>
              </a>

            </div>

          </div>
        </div>
        <!-- Immunity Booster Dropdown End Here-->

      </a>
      <!-- Immunity Booster Menu End Here-->

      <!-- Cold & Headache Menu Start Here-->
      <a href="/default/cold-headache.html" class="sf-link sf-header-navigation-item__link nav-item custom_menu menu6" 
              @mouseenter="showDropdown5"
              @mouseleave="handleMouseLeave5"
            > Cold & Headache

        <span class="sf-icon color-green-primary size-xxs" style="">
          <svg viewBox="0 0 24 24" preserveAspectRatio="none" class="sf-icon-path">
            <defs class="">
              <linearGradient id="linearGradient-39" x1="0" y1="0" x2="1" y2="0">
                <stop offset="1" stop-color="var(--icon-color)"></stop>
                <stop offset="0" stop-color="var(--icon-color-negative, var(--c-gray-variant))"></stop>
              </linearGradient>
            </defs>
            <path d="M2 8.364L3.6 7l8.4 7.254L20.4 7 22 8.364 12 17z" fill="var(--icon-color)" style="height: 100%;"></path>
          </svg>
        </span> 

        <!-- Cold & Headache Dropdown Here-->
        <div class="header-navigation__subcategories custom_dropdown menu2_dropdown"  v-if="isDropdownVisible5" @mouseenter="showDropdown5"
        @mouseleave="hideDropdown5">
          <div class="header-navigation__subcategories-inner">


            <div class="header-navigation__subcategory">
              <SfLink class="header-navigation__link1" link='/default/looloo-oleo-cold-shield-roll-on-oil-with-kalonji.html'>
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Cold Shield Roll-On Oil with Kalonji</h2>
              </SfLink>
              <SfLink class="header-navigation__link1" link='/default/cold-relief-offer-pack-of-3.html'>
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">Cold Relief Offer Pack of 3</h2>
              </SfLink>
              <SfLink class="header-navigation__link1" link='/default/looloo-oleo-cold-shield-roll-on-oil-with-kalonji-pack-of-8.html'>
                <h2 class="sf-heading sf-heading--left sf-heading sf-heading--left h5">LooLoo Oleo Cold Shield Roll-On Oil with Kalonji Pack of 8</h2>
              </SfLink>
            </div>

          </div>
        </div>
        <!-- Cold & Headache Dropdown End Here-->

      </a>
       <!-- Cold & Headache Menu End Here-->

    </div>
    <!-- <HeaderNavigationSubcategories
      v-if="hasChildren(currentCategory)"
      :current-category="currentCategory"
      :has-focus="hasFocus"
      @hideSubcategories="focusRootElementAndHideSubcategories"
    /> -->
  </div>
</template>
<script lang="ts">
import {
  defineComponent, PropType, ref, 
} from '@nuxtjs/composition-api';
import {
  SfLink, SfList,
} from '@storefront-ui/vue';
import { CategoryTree } from '~/modules/GraphQL/types';
import { useUiHelpers } from '~/composables';
import type { ComponentTemplateRef } from '~/types/componentTemplateRef';
import HeaderNavigationItem from './HeaderNavigationItem.vue';
import Dropdown_arrow_svg from './dropdown_arrow_svg.vue';
import Oral_care_menu from './oral_care_menu.vue';


export default defineComponent({
  name: 'HeaderNavigation',
  components: {
    HeaderNavigationSubcategories: () => import('~/components/Header/Navigation/HeaderNavigationSubcategories.vue'),
    HeaderNavigationItem,
    SfLink,
    SfList,
  },
  props: {
    categoryTree: {
      type: Array as PropType<CategoryTree[]>,
      default: () => [],
    },
  },
  setup() {
    const { getCatLink } = useUiHelpers();

    // State to track dropdown visibility
    const isDropdownVisible = ref(false);
    const isDropdownVisible1 = ref(false);
    const isDropdownVisible2 = ref(false);
    const isDropdownVisible3_3rdLevel = ref(false);
    const isDropdownVisible4_3rdLevel = ref(false);
    const isDropdownVisible5_3rdLevel = ref(false);
    const isDropdownVisible5_1_3rdLevel = ref(false);
    const isDropdownVisible3 = ref(false);
    const isDropdownVisible4 = ref(false);
    const isDropdownVisible5 = ref(false);

    // Functions to handle mouse events
    const showDropdown = () => {
      isDropdownVisible.value = true;
      isDropdownVisible1.value = false
      isDropdownVisible2.value = false
      isDropdownVisible3.value = false
      isDropdownVisible4.value = false
      isDropdownVisible5.value = false
    };
    const showDropdown1 = () => {
      isDropdownVisible.value = false;
      isDropdownVisible1.value = true;
      isDropdownVisible2.value = false
      isDropdownVisible3.value = false
      isDropdownVisible4.value = false
      isDropdownVisible5.value = false
    };
    const showDropdown2 = () => {
      isDropdownVisible.value = false;
      isDropdownVisible1.value = false;
      isDropdownVisible2.value = true
      isDropdownVisible3_3rdLevel.value = false; // Close 3rd level
      isDropdownVisible3.value = false
      isDropdownVisible4.value = false
      isDropdownVisible5.value = false
      
      console.log('1 level menu');
    };
    const showDropdown3_3rdLevel = () => {
      isDropdownVisible3_3rdLevel.value = true;
    };

    const showDropdown4_3rdLevel = () => {
      isDropdownVisible4_3rdLevel.value = true;
    };

    const showDropdown5_3rdLevel = () => {
      isDropdownVisible5_3rdLevel.value = true;
    };
    const showDropdown5_1_3rdLevel = () => {
      isDropdownVisible5_1_3rdLevel.value = true;
    };

    const showDropdown3 = () => {
      isDropdownVisible.value = false;
      isDropdownVisible1.value = false;
      isDropdownVisible2.value = false
      isDropdownVisible3.value = true
      isDropdownVisible4_3rdLevel.value = false; // Close 3rd level
      isDropdownVisible4.value = false
      isDropdownVisible5.value = false
    };
    const showDropdown4 = () => {
      isDropdownVisible.value = false;
      isDropdownVisible1.value = false;
      isDropdownVisible2.value = false
      isDropdownVisible3.value = false
      isDropdownVisible4.value = true
      isDropdownVisible5_3rdLevel.value = false; // Close 3rd level
      isDropdownVisible5_1_3rdLevel.value = false; // Close 3rd level
      isDropdownVisible5.value = false
    };
    const showDropdown5 = () => {
      isDropdownVisible.value = false;
      isDropdownVisible1.value = false;
      isDropdownVisible2.value = false
      isDropdownVisible3.value = false
      isDropdownVisible4.value = false
      isDropdownVisible5.value = true
    };

// --------------------------------------------------------

    const hideDropdown = () => {
      isDropdownVisible.value = false;
    };
    const hideDropdown1 = () => {
      isDropdownVisible1.value = false;
    };
    const hideDropdown2 = () => {
      isDropdownVisible2.value = false;
      isDropdownVisible3_3rdLevel.value = false; // Close 3rd level
    };
    const hideDropdown3_3rdLevel = () => {
      isDropdownVisible3_3rdLevel.value = false;
    };
    const hideDropdown4_3rdLevel = () => {
      isDropdownVisible4_3rdLevel.value = false;
    };
    const hideDropdown5_3rdLevel = () => {
      isDropdownVisible5_3rdLevel.value = false;
    };
    const hideDropdown5_1_3rdLevel = () => {
      isDropdownVisible5_1_3rdLevel.value = false;
    };
    const hideDropdown3 = () => {
      isDropdownVisible3.value = false;
    };
    const hideDropdown4 = () => {
      isDropdownVisible4.value = false;
    };
    const hideDropdown5 = () => {
      isDropdownVisible5.value = false;
    };

// --------------------------------------------------------

    const handleMouseLeave = () => {
      setTimeout(() => {
        if (!isDropdownVisible.value) hideDropdown();
      }, 300); // Slight delay to avoid flicker on fast mouse movements
    };
    const handleMouseLeave1 = () => {
      setTimeout(() => {
        if (!isDropdownVisible1.value) hideDropdown();
      }, 300); // Slight delay to avoid flicker on fast mouse movements
    };
    const handleMouseLeave2 = () => {
      setTimeout(() => {
        if (!isDropdownVisible2.value) hideDropdown();
      }, 300); // Slight delay to avoid flicker on fast mouse movements
    };
    const handleMouseLeave3 = () => {
      setTimeout(() => {
        if (!isDropdownVisible3.value) hideDropdown();
      }, 300); // Slight delay to avoid flicker on fast mouse movements
    };
    const handleMouseLeave4 = () => {
      setTimeout(() => {
        if (!isDropdownVisible4.value) hideDropdown();
      }, 300); // Slight delay to avoid flicker on fast mouse movements
    };
    const handleMouseLeave5 = () => {
      setTimeout(() => {
        if (!isDropdownVisible5.value) hideDropdown();
      }, 300); // Slight delay to avoid flicker on fast mouse movements
    };

// --------------------------------------------------------
    const currentCategory = ref<CategoryTree | null>(null);
    const lvl0CatRefs = ref<ComponentTemplateRef[]>();
    const hasFocus = ref(false);
    let lvl0CatFocusIdx = 0;
    let focusedElement : HTMLElement | null = null;

    const setCurrentCategory = (category: CategoryTree | null) => {
      currentCategory.value = category;
    };

    const hasChildren = (category: CategoryTree) => Boolean(category?.children?.length);

    const setFocus = (event: MouseEvent & { target: HTMLElement }) => {
      focusedElement = event.target;
      lvl0CatFocusIdx = Number(event.target.dataset.index);
      hasFocus.value = true;
    };

    const focusRootElementAndHideSubcategories = () => {
      setCurrentCategory(null);
      if (focusedElement !== null) focusedElement.focus();
    };

    const navRight = () => {
      lvl0CatFocusIdx++;
      if (lvl0CatRefs.value[lvl0CatFocusIdx]) {
        lvl0CatRefs.value[lvl0CatFocusIdx].$el.focus();
        focusedElement = lvl0CatRefs.value[lvl0CatFocusIdx].$el;
      } else {
        lvl0CatFocusIdx--;
      }
    };

    const navLeft = () => {
      lvl0CatFocusIdx--;
      if (lvl0CatRefs.value[lvl0CatFocusIdx]) {
        lvl0CatRefs.value[lvl0CatFocusIdx].$el.focus();
        focusedElement = lvl0CatRefs.value[lvl0CatFocusIdx].$el;
      } else {
        lvl0CatFocusIdx++;
      }
    };

    const onMouseEnter = async (category: CategoryTree) => {
      console.log('Category Data:', category);

      currentCategory.value = category;
      focusedElement = null;
      hasFocus.value = false;
    };

    return {
      getCatLink,
      setCurrentCategory,
      currentCategory,
      hasChildren,
      setFocus,
      focusRootElementAndHideSubcategories,
      lvl0CatRefs,
      navRight,
      navLeft,
      hasFocus,
      onMouseEnter,
      isDropdownVisible,
      showDropdown,
      hideDropdown,
      handleMouseLeave,

      isDropdownVisible1,
      showDropdown1,
      hideDropdown1,
      handleMouseLeave1,

      isDropdownVisible2,
      showDropdown2,
      hideDropdown2,
      handleMouseLeave2,

      isDropdownVisible3,
      showDropdown3,
      hideDropdown3,
      handleMouseLeave3,

      isDropdownVisible4,
      showDropdown4,
      hideDropdown4,
      handleMouseLeave4,

      isDropdownVisible5,
      showDropdown5,
      hideDropdown5,
      handleMouseLeave5,

      isDropdownVisible3_3rdLevel,
      showDropdown3_3rdLevel,
      hideDropdown3_3rdLevel,

      isDropdownVisible4_3rdLevel,
      showDropdown4_3rdLevel,
      hideDropdown4_3rdLevel,

      isDropdownVisible5_3rdLevel,
      showDropdown5_3rdLevel,
      hideDropdown5_3rdLevel,

      isDropdownVisible5_1_3rdLevel,
      showDropdown5_1_3rdLevel,
      hideDropdown5_1_3rdLevel,


    };
  },
});
</script>

<style>
  .desk_3rd_level_dp {
    top: -15px;
    right: -116% !important;
  } 
  .desk_3rd_level_menu {
    position: relative;
  }
  .desk_3rd_level_menu::after {
    content: '';
    position: absolute;
    width:10px;
    height:10px;
    background-image:url('../../../static/dropdown_arrow.png');
    background-repeat: no-repeat;
    background-size: 13px;
    background-position: center;
    right: 6px;
    top: 41%;
  }
  .header-navigation__subcategories{
    position: absolute;
    z-index: 1;
    background-color: #fff;
    box-shadow: 0 3px var(--c-primary);
    left: 0;
    width: 220px;
    padding: 10px 10px 10px 10px;
    right: 0;
    top: 85px;
    flex-wrap: wrap;
    justify-content: center;
    display: flex;
    box-shadow: 0px 0px 4px rgba(0, 0, 0, .2);
    box-sizing: border-box;
}
.header-navigation__subcategories-inner{
    width:100%;
}
/* .header-navigation__subcategory {
    flex: 0 0 25%;
}
.header-navigation .sf-link {
    text-decoration: none;
} */
.menubar .header-navigation .custom_dropdown a {
    height: auto;
    margin: 0;
    display: block;
}
.menubar .header-navigation .custom_dropdown a h2{
    font-size: 14px;
    line-height: 18px;
    color: #978d4b;
    font-family: "Montserrat", sans-serif;
    font-weight: 400;
    padding: 10px 10px 10px 10px;
    border-top:1px solid #0000001c;
    text-transform: capitalize;
}
.menubar .header-navigation .custom_dropdown a h2:hover{
  color:#05923f ;
}
.menubar .header-navigation .custom_dropdown a:first-child h2 {
  border-top:0px solid #0000001c;
}
.desk_3rd_level_dropdown {
    top: 0px;
    right: -110%;
    left: auto;
}
.top_3rd_dp {
    top: -10px;
}
</style>

<style lang="scss" scoped>
.header-navigation {
  &__main {
    display: flex;
  }
}
.nav-item {
  --header-navigation-item-margin: 0 var(--spacer-sm);

  .sf-header-navigation-item__item--mobile {
    display: none;
  }
}
</style>
