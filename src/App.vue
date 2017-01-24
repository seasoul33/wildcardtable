<template>
    <div id="app">
        <!-- <img src="./assets/logo.png"> -->
        <tableform v-bind:dataSource={vlan}></tableform>
    </div>
</template>

<script>
import tableform from './components/tableform'
var sourceData = { 
              vlan: {
                name: 'VLAN table',

                options: {
                    rawAction: true,
                    rawActionType: 'checkbox',
                    columnAction: true,
                },
                
                column: [
                    {
                        columnName: 'VID',
                        columnActionType: 'checkbox',
                        columnActionOptions: ['A','B','C'],
                    },
                    {
                        columnName: 'Name',
                        columnActionType: 'none',
                        columnActionOptions: ['1','2','3'],
                    },
                    {
                        columnName: 'member',
                        columnActionType: 'dropdown',
                        columnActionOptions: ['a','b','c'],
                    }
                ],
                
                data: [
                        [1, 'default', [1,3,5]],
                        [2, 'guest', [2,4]]
                ],

                restUrl: [
                ]
              },

              FDB: {
                name: 'FDB table',

                options: {
                    rawAction: true,
                    rawActionType: 'checkbox',
                    columnAction: false,
                },
                
                column: [
                    {
                        columnName: 'MAC',
                        columnActionType: 'checkbox',
                        columnActionOptions: ['A','B','C'],
                    },
                    {
                        columnName: 'Port',
                        columnActionType: 'none',
                        columnActionOptions: ['1','2','3'],
                    },
                    {
                        columnName: 'VLAN',
                        columnActionType: 'dropdown',
                        columnActionOptions: ['a','b','c'],
                    }
                ],
                
                data: [
                        ['00:01:02:03:04:05', [1,2], 1],
                        ['00:01:02:03:17:16', 10, 5],
                        ['00:01:02:03:17:16', 11, 1],
                        ['00:01:11:55:11:22', 25, 100],
                ],

                restUrl: [
                ]
              }
            }
export default {
    name: 'app',
    components: {
        tableform
    },
    data: function (){
        return sourceData;
    }
}
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
