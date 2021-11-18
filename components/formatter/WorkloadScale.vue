<script>
import Vue from 'vue';
import PlusMinus from '@/components/form/PlusMinus';
import { SCALABLE_WORKLOAD_TYPES } from '@/config/types';

const SCALABLE_TYPES = Object.values(SCALABLE_WORKLOAD_TYPES);

export default {
  components: { PlusMinus },

  props: {
    row: {
      type:     Object,
      required: true
    },
  },

  data() {
    return { disabled: false };
  },

  computed: {
    canScale() {
      return !!SCALABLE_TYPES.includes(this.row.type);
    }
  },

  methods: {
    async scaleDown() {
      Vue.set(this, 'disabled', true);
      await this.row.scaleDown();
      Vue.set(this, 'disabled', false);
    },
    async scaleUp() {
      Vue.set(this, 'disabled', true);
      await this.row.scaleUp();
      Vue.set(this, 'disabled', false);
    },
  },

};
</script>

<template>
  <PlusMinus v-if="canScale" :value="row.spec.replicas" :disabled="disabled" @minus="scaleDown" @plus="scaleUp" />
</template>
