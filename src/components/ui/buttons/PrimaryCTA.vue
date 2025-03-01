<template>
  <!-- Link styled as a button, with dynamic title, URL, and optional arrow -->
  <a
    :class="[baseClasses, borderClasses, bgColorClasses, disableClasses, fontSizeClasses, ringClasses, { 'disabled:pointer-events-none disabled:opacity-50': isDisabled }]"
    :href="url"
  >
    {{ computedTitle }}
    <!-- Display the arrow based on the 'noArrow' property -->
    <Icon v-if="!noArrow" name="arrowRight" />
  </a>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue';
import Icon from '@components/ui/icons/Icons.vue';

export default defineComponent({
  components: {
    Icon,
  },
  props: {
    title: {
      type: String,
      default: '',
    },
    url: {
      type: String,
      default: '/contact',
    },
    noArrow: {
      type: Boolean,
      default: false,
    },
    isDisabled: {
      type: Boolean,
      default: false,
    },
  },
  setup(props) {
    // Reactive refs to hold the prop values
    const computedTitle = ref(props.title);
    const computedUrl = ref(props.url);

    // Watchers to update the refs when the props change
    watch(
      () => props.title,
      (newTitle) => {
        computedTitle.value = newTitle;
      }
    );

    // Define CSS classes for styling the button
    const baseClasses =
      'group inline-flex items-center justify-center gap-x-2 rounded-lg px-4 py-3 text-sm font-bold text-neutral-50 ring-zinc-500 transition duration-300 focus-visible:ring outline-none';
    const borderClasses = 'border border-transparent';
    const bgColorClasses =
      'bg-orange-400 hover:bg-orange-500 active:bg-orange-500 dark:focus:outline-none';
    const disableClasses = 'disabled:pointer-events-none disabled:opacity-50';
    const fontSizeClasses = '2xl:text-base';
    const ringClasses = 'dark:ring-zinc-200';

    return {
      computedTitle,
      computedUrl,
      baseClasses,
      borderClasses,
      bgColorClasses,
      disableClasses,
      fontSizeClasses,
      ringClasses,
    };
  },
});
</script>
