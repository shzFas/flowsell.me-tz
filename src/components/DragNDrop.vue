<script setup>
import { VueFlow } from '@vue-flow/core'
import { Panel, PanelPosition, useVueFlow } from '@vue-flow/core'
import { ref } from 'vue'
import { Controls } from '@vue-flow/controls'
const flowKey = 'allchanges'

const { nodes, addNodes, setNodes, setEdges, dimensions, setTransform, toObject, addEdges, onConnect } = useVueFlow()

onConnect((params) => addEdges([params]))
const elements = ref([]);

const onSave = () => {
  localStorage.setItem(flowKey, JSON.stringify(toObject()));
  console.log(elements);
}

const onRestore = () => {
  const flow = JSON.parse(localStorage.getItem(flowKey))

  if (flow) {
    const [x = 0, y = 0] = flow.position
    setNodes(flow.nodes)
    setEdges(flow.edges)
    setTransform({ x, y, zoom: flow.zoom || 0 })
  }
}

const onAdd = () => {
  const id = nodes.value.length + 1

  const newNode = {
    id: `random_node-${id}`,
    label: `Node ${id}`,
    position: { x: 0 * dimensions.value.width, y: 0 * dimensions.value.height },
  }

  addNodes([newNode])
}
</script>

<template>
  <VueFlow v-model="elements">
    <Controls />
    <Panel :position="PanelPosition.TopRight" class="save-restore-controls">
      <button style="background-color: #33a6b8" @click="onSave">save</button>
      <button style="background-color: #113285" @click="onRestore">restore</button>
      <button style="background-color: #6f3381" @click="onAdd">add node</button>
    </Panel>
  </VueFlow>
</template>
