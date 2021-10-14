<template>
  <div class="hello">
    $props.modelValue : {{ $props.modelValue }}
    <br>
    <button
      @click="plusTwoValue"
    >
      +2
    </button>
  </div>
</template>

<script>
import { computed } from 'vue';

export default {
  name: 'ReactiveComp',
  props: {
    modelValue: {
      type: Number,
      default: 0,
    },
  },
  emits: {
    'update:modelValue': (val) => {
      if (!Number.isNaN(val)) {
        return true;
      }
      console.warn('숫자가 아닙니다.');
      return false;
    },
  },
  setup(props, { emit }) {
    const currentValue = computed({
      get: () => props.modelValue,
      set: (val) => emit('update:modelValue', val),
    });

    const plusTwoValue = () => {
      emit('update:modelValue', currentValue.value + 2);
    };

    return {
      plusTwoValue,
    };
  },
};
</script>
