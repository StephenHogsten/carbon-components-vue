<!--
  An item in a Carbon accordion.

  Usage:
    See accordion.vue
-->

<template>
  <li
    data-accordion-item
    class="cv-accordion-item bx--accordion__item"
    :class="{ 'bx--accordion__item--active': dataOpen }"
  >
    <button
      class="bx--accordion__heading"
      :aria-expanded="`${dataOpen}`"
      :aria-controls="uid"
      @click="toggle"
    >
      <svg
        class="bx--accordion__arrow"
        width="8"
        height="12"
        viewBox="0 0 8 12"
        fill-rule="evenodd"
      >
        <path d="M0 10.6L4.7 6 0 1.4 1.4 0l6.1 6-6.1 6z"></path>
      </svg>
      <p class="bx--accordion__title"><slot name="title"></slot></p>
    </button>
    <div :id="uid" class="bx--accordion__content">
      <slot name="content"></slot>
    </div>
  </li>
</template>

<script>
import uidMixin from '../../mixins/uid-mixin';

export default {
  name: 'CvAccordionItem',
  mixins: [uidMixin],
  props: {
    open: { type: Boolean, default: false },
  },
  mounted() {
    this.dataOpen = this.open;
  },
  watch: {
    open(val) {
      this.dataOpen = val;
    },
  },
  data() {
    return {
      dataOpen: false,
    };
  },
  methods: {
    toggle(force) {
      if (typeof force === 'boolean') {
        this.dataOpen = force === true;
      } else {
        this.dataOpen = !this.dataOpen;
      }
    },
  },
};
</script>

<style lang="scss"></style>
