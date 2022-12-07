<template>

    <Grid
          ref="grid"
          
          :style="{height: '520px'}"
          :data-items="products"
          :selected-field="selectedField"
          :columns="columns"
         header = hidden;
          @selectionchange="onSelectionChange"
          @rowclick="onRowClick">
      </Grid>

      <tc-stock-list :exch="exch"></tc-stock-list>
  </template>
  
  <script>
  import { Grid } from '@progress/kendo-vue-grid';
  import '@progress/kendo-theme-default/dist/all.css';
  import TcStockList from "./TcStockList.vue";
 
  export default {
      components: {
         TcStockList,
          'Grid': Grid
      },
      props: ["exchlist"],
      data() {
          return {

             exch:[],
              selectedField: 'selected',
              products: this.exchlist,
             
              staticColumns: [
                
                  { field: 'id',  width: '150px', },
                  { field: 'name' , },
                  { field: 'status', },
                  { field: 'GMT', }
              ]
          };
      },
      watch:{

      },
      mounted() {
          this.hideDetailGridHeaders();
      },
      methods: {
        hideDetailGridHeaders() {
      (".k-grid tbody .k-grid .k-grid-header").hide();
  },
          onHeaderSelectionChange (event) {
              let checked = event.event.target.checked;
              this.products = this.products.map((item) => { return {...item, selected: checked} });
              if(this.selected ===true){
                    this.exch.push(this.products)

              }
              else if(this.selected ===false){
                  this.exch.splice(this.exch.indexOf(this.products),1)
              }
             
          },

          onSelectionChange (event) {
              event.dataItem[this.selectedField] = !event.dataItem[this.selectedField];
              if(event.dataItem[this.selectedField] == false)
              {
                  this.exch.splice(this.exch.indexOf(event.dataItem),1)
              }
              else
              this.exch.push(event.dataItem)
              console.log(this.exch)
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
  <style>
  .k-grid tbody .k-grid .k-grid-header
{
    display: none;
}
</style>