<script setup>
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";
import 'ag-grid-enterprise';
import { AgGridVue } from "ag-grid-vue3";
import { onBeforeMount, ref } from "vue";
import DetailCellRenderer from './DetailCellRenderer.vue'

const rowData = ref([
  { rowId: 1, name: "Carlos", age: "20", country: "Cuba", email: 'carlos@gmail.com' },
  { rowId: 2, name: "Laura", age: "50", country: "Cuba", email: 'laura@gmail.com' },
  { rowId: 3, name: "Adrián", age: "22", country: "Estados Unidos", email: 'adrian@gmail.com' },
  { rowId: 4, name: "Violeta", age: "16", country: "España", email: 'violeta@gmail.com' },
  { rowId: 5, name: "Roberto", age: "35", country: "Francia", email: 'roberto@gmail.com' },
  { rowId: 6, name: "Alicia", age: "20", country: "Cuba", email: 'alicia@gmail.com' },
  { rowId: 7, name: "Enrique", age: "60", country: "Cuba", email: 'enrique@gmail.com' },
  { rowId: 8, name: "Daniela", age: "32", country: "Estados Unidos", email: 'daniela@gmail.com' },
  { rowId: 9, name: "Gabriel", age: "16", country: "España", email: 'gabriel@gmail.com' },
  { rowId: 10, name: "Alberto", age: "25", country: "Francia", email: 'alberto@gmail.com' },
]);

const columnDefs = ref(
  [
    { headerName: "Nombre", field: "name", cellRenderer: "agGroupCellRenderer", rowDrag: true },
    { headerName: "Edad", field: "age" },
    { headerName: "País", field: "country" },
    { headerName: "Correo", field: "email" },
  ],
);

const defaultColDef = ref({
  sortable: true,
  filter: true,
  resizable: true,
  width: 195,
})

const detailCellRendererParams = ref({
  getDetailRowData: params => {
    params.successCallback(params.data.callRecords);
  }
})

const context = ref({})

const updateRows = (row) => {
  const index = rowData.value.findIndex(item => item.rowId === row.rowId);
  if (index !== -1) {
    rowData.value = [
      ...rowData.value.slice(0, index),
      { ...row },
      ...rowData.value.slice(index + 1)
    ];
  }
};

onBeforeMount(() => {
  context.value = {
    componentParent: {
      updateRows
    }
  }
})

</script> 

<template>
  <div class="grid-container">
    <ag-grid-vue class="ag-theme-alpine-dark" style="height: 500px;" :detailCellRendererParams="detailCellRendererParams"
      :detailCellRenderer="DetailCellRenderer" :defaultColDef="defaultColDef" :masterDetail="true"
      :columnDefs="columnDefs" :rowData="rowData" :rowDragManaged="true" :animateRows="true" :context="context"
      detailRowHeight="80">
    </ag-grid-vue>
  </div>
</template>

<style>
.grid-container {
  width: 800px;
}

.ag-root-wrapper.ag-layout-normal {
  border-radius: 5px;
}
</style>
