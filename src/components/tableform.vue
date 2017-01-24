<template>
  <div class="tableform">
    <h1>{{ title }}</h1>

    <!-- <h3>props test -> {{test}}</h3>
    <h3>second -> {{topNode}}</h3> -->

    <table border="1">
        <caption>{{topNode.name}}</caption>
        <tr>
            <th v-if="topNode.options.rawAction"></th>
            <th v-for="item of topNode.column">{{item.columnName}}</th> 
        </tr>
        <tr v-if="topNode.options.columnAction">
            <td></td>
            <td v-for="(item, colIndex) of topNode.column.length">
                <span v-if="topNode.column[colIndex].columnActionType === 'checkbox'">
                    <input :name="colIndex" type="checkbox" :value="colIndex" v-model="colSelectedData">
                </span>
                <span v-else-if="topNode.column[colIndex].columnActionType === 'radio'">
                    <input :name="colIndex" type="radio" :value="colIndex" v-model="colSelectedData">
                </span>
                <span v-else-if="topNode.column[colIndex].columnActionType === 'dropdown'">
                    <select :name="colIndex" v-model="colSelectedMultiData[colIndex]">
                        <option v-for="option of topNode.column[colIndex].columnActionOptions">{{option}}</option>
                    </select>
                </span>
            </td>
        </tr>
        <tr v-for="(item, rawIndex) of topNode.data">
            <td v-if="topNode.options.rawAction">
                <input v-if="topNode.options.rawActionType === 'checkbox'" type="checkbox" :value="rawIndex" v-model="rawSelectedData">
                <input v-else-if="topNode.options.rawActionType === 'radio'" type="radio" :value="rawIndex" v-model="rawSelectedData">
            </td>
            <td v-for="value of item">
                <span v-if="Array.isArray(value)">
                    <span v-for="element of value">
                        {{element}}
                    </span>
                </span>
                <span v-else>
                    {{value}}
                </span>
            </td>
        </tr>
    </table>
    column action: {{colSelectedData}} + {{colSelectedMultiData}}<br/>
    raw action: {{rawSelectedData}}

  </div>
</template>

<script>
export default {
    name: 'tableform',
    props: {
        dataSource: {
            type: Object
        }
    },
    data () {
        return {
            title: 'Wildcard Table+Form Component',
            rawSelectedData: [],
            colSelectedData: [],
            colSelectedMultiData: Array.from({ length: this.dataSource[Object.keys(this.dataSource)[0]].column.length }, () => []),
        }
    },
    computed: {
        topNode: function() {
            return this.dataSource[Object.keys(this.dataSource)[0]];
        },
    },
    methods: {
        
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>
