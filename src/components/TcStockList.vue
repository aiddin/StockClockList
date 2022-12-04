<template>
    <table class="w-4/5   m-auto">
    
        <tr class="border-thin border-2 border-gray-600  " v-for="server in servers" v-bind:key="server.id">
            <th class="">
                <TcStockStat v-bind:icon="exch.status" />
            </th>
            <th class=" text-left w-1/10 ">
                <h1 class="text-2xl">{{(exch.name)}}</h1>
                <a class="text-sm ">{{exch.gmTime}}</a>
            </th>
            
        </tr>
    
    </table>
    </template>
    
    <script>
    import TcClock from '../components/TcClock.vue'
    import TcStockStat from '../components/TcStockStat.vue'
    export default {
        components: {
            TcClock,
            TcStockStat
        },
        props: [
            'servers'
        ]
    }
    </script>
    
    <!-- Add "scoped" attribute to limit CSS to this component only -->
    
    <style>
    th {
        padding-right: 15px;
        padding-left: 15px;
        padding-bottom: 15px;
    }
    </style>
    