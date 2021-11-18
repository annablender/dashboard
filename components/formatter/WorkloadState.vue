<script>
import ProgressBarMulti from '@/components/ProgressBarMulti';
import { ucFirst } from '~/utils/string';

export default {
  components: { ProgressBarMulti },

  props: {
    row: {
      type:     Object,
      required: true
    },
  },

  computed: {
    parts() {
      return Object.entries( this.row.jobGauges || this.row.podGauges || [])
        .map(([name, value]) => ({
          color:     `bg-${ value.color }`,
          value:     value.count || 0,
          tooltip:   `${ ucFirst(name) }\n: ${ value.count || 0 }`,
        }))
        .filter(x => x.value > 0);
    }
  },

  methods: {}
};
</script>

<template>
  <ProgressBarMulti v-if="parts" :values="parts" :show-zeros="true" />
</template>
