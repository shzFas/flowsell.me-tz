<script lang="ts" setup>
import { VueFlow } from '@vue-flow/core'
import { ref } from 'vue'
import SaveRestoreControls from './components/Controls.vue';
import { Controls } from '@vue-flow/controls'
import './style.css';

const elements = ref([{ id: '1', label: 'Node 1', position: { x: 100, y: 100 } }])
</script>

<template>
  <VueFlow v-model="elements">
    <SaveRestoreControls />
    <Controls />
  </VueFlow>
</template>