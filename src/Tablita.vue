<template>
    <table class="table table-bordered">
        <thead>
        <tr>
            <th>Query</th>
            <th>Tiempo de Ejecución</th>
            <th>PEV</th>
        </tr>
        </thead>
        <tr v-for="item in items" v-bind:key="item.id">
            <td>{{item.query}}</td>
            <td>{{item.tiempo}}</td>
            <td>
                <router-link :to="{ name: 'pev', params: {}}">PEV</router-link>
            </td>
        </tr>
    </table>
</template>

<script>
    export default {
        name: "Tablita",
        data:function() {
            return {
                items: [] // initialise to an empty array
            }
        },
        created: function () {
            this.getLogData().then(result => {
                this.items = result;
            });
        },
        methods: {
            getLogData: async function () {
                const res = await fetch("https://run.mocky.io/v3/f7632241-39fc-4c9e-b427-b865fe2d6b83", {
                    method: 'GET',
                    headers: {
                        "Accept": "application/json"
                    }
                });

                return res.json();
            }
        }
    }
</script>

<style lang="scss">
    html,
    body,
    #app {
        height: 100%;
    }
</style>