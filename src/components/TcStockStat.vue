<template>
        <div v-bind:status="status">

    </div>

    </template>
    
    <script>
    export default {
        props: [
            'icon'
        ],
        data() {
            return {
                status: {
                    message: 'testmessage',
                   
                }
    
            }
        },
        created() {
            this.test()
        },
        methods: {
            test() {
                if (this.icon == 0) {
                    this.status = {
                        message: 'open',
                        color: 'bg-green-500'
                    }
                } else if (this.icon == 1) {
                    this.status = {
                       message: 'close',
                        color: 'bg-red-500'
                    }
                } else {
                    this.status = {
                        message: 'break',
                        color: 'bg-orange-500'
                    }
                }
    
            }
    
        }
    }
    </script>
    
 <style>
 
</style>