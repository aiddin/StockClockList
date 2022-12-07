<template>

    <Grid
          ref="grid"
          :style="{height: '520px'}"
          :data-items="exchange"
          :selected-field="selectedField"
          :columns="columns"
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
              exchange: this.exchlist,
             
              staticColumns: [
                  { field: 'id', title:'ID', width: '150px' },
                  { field: 'name', title: 'Exchange Name' },
                  { field: 'status',  title: 'Status' },
                  { field: 'GMT', title: 'Greenwich Mediteraenan Time' },
          ]
          };
      },
      computed: {//this function is used to select all the rows in the grid
         
          columns () {
              return [
                  { field: 'selected', width: '50px', headerSelectionValue: this.areAllSelected },
                  ...this.staticColumns
              ]
          }
      },
      methods: {
       
          onHeaderSelectionChange (event) {
              let checked = event.event.target.checked;
              this.exchange = this.exchange.map((item) => { return {...item, selected: checked} });
              if(this.selected ===true){
                    this.exch.push(this.exchange)

              }
              else if(this.selected ===false){
                  this.exch.splice(this.exch.indexOf(this.exchange),1)
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