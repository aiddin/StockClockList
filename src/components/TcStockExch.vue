<template>
    <tc-stock-list :exch="exch"></tc-stock-list>
    <Grid
          ref="grid"
          :style="{height: '520px'}"
          :data-items="products"
          :selected-field="selectedField"
          :columns="columns"
          @selectionchange="onSelectionChange"
          @headerselectionchange="onHeaderSelectionChange"
          @rowclick="onRowClick">
      </Grid>
  </template>
  
  <script>
  import { Grid } from '@progress/kendo-vue-grid';
  import { products } from './exchange.js';
  import TcStockList from "./TcStockList.vue";
  export default {
      components: {
         TcStockList,
          'Grid': Grid
      },
      data: function () {
          return {
             exch:[],
              selectedField: 'selected',
              products: products.map(item => { return {...item, selected: false} }),
              staticColumns: [
                  { field: 'id',  width: '150px' },
                  { field: 'name' },
                  { field: 'status', },
                  { field: 'GMT'}
              ]
          };
      },
      computed: {
          areAllSelected () {
              return this.products.findIndex(item => item.selected === false) === -1;
          },
          columns () {
          
              return [
                  { field: 'selected', width: '50px', headerSelectionValue: this.areAllSelected },
                  ...this.staticColumns,
                
                  
              ]
          }
      },
      methods: {
        
          onHeaderSelectionChange (event) {
              let checked = event.event.target.checked;
              this.products = this.products.map((item) => { return {...item, selected: checked} });
          },
          onSelectionChange (event) {
              event.dataItem[this.selectedField] = !event.dataItem[this.selectedField];
          },
          onRowClick (event) {
           
              event.dataItem[this.selectedField] = !event.dataItem[this.selectedField];
              if(event.dataItem[this.selectedField] == false)
              {
                  this.exch.splice(this.exch.indexOf(event.dataItem),1)
              }
              else
              this.exch.push(event.dataItem)
              console.log(this.exch)
          },
          
      }
  };
  
  </script>