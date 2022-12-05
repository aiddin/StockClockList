<template>
        <div v-bind:stat="status">
            {{ status.message }}

    </div>

    </template>
    
    <script>
    export default {
        props: [
            'stat'
        ],
        data() {
            return {
                message : this.status,
            }
        },
        created() {
            this.test()
        },
        methods: {
            test() {
                if (this.stat == 0) {
                    this.status = {
                        message: 'open',
                    }
                } else if (this.stat == 1) {
                    this.status = {
                       message: 'close',
                       
                    }
                } else if (this.stat == 2) {
                    this.status = {
                        message: 'break',
                        
                    }
                }
    
            }
    
        }
    }
    </script>
    
 <style>
 
</style>