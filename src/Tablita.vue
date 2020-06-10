<template>
    <div>
        <br>
        <br>
        <div class="container">
            <div class="row">
                <div class="col-sm">
                    <div class="form-group container">
                        <label for="slFile">API Endpoints</label>
                        <select class="form-control" id="slFile" name="slFile"
                                v-model="endpointSelected"
                                @change="getFile()">
                            <option value="">Selecciona</option>
                            <option value="1">/auth</option>
                            <option value="2">/actions/access/{idact}</option>
                            <option value="3">/actions/access/{idact}/applications/{idapp}</option>
                            <option value="4">/actions/available</option>
                            <option value="5">/actions/allowedButtons</option>
                        </select>
                    </div>
                </div>
                <div class="col-sm">
                </div>
                <div class="col-sm">
                </div>
            </div>
        </div>

        <table class="table table-bordered container">
            <thead>
            <tr>
                <th>Query</th>
                <th>Tiempo de Ejecución</th>
                <th>PEV</th>
            </tr>
            </thead>
            <tr v-for="item in items" v-bind:key="item.id">
                <td>{{item.query}}</td>
                <td><span class="badge badge-danger">{{item.tiempo}}</span></td>
                <td>
                    <router-link :to="{ name: 'pev', params: {}}">PEV</router-link>
                </td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: "Tablita",
        data: function () {
            return {
                items: [], // initialise to an empty array
                endpointSelected: ""
            }
        },
        /*created: function () {
        },*/
        methods: {
            getLogData: async function (endpointSelected) {
                //const res = await fetch("https://run.mocky.io/v3/f7632241-39fc-4c9e-b427-b865fe2d6b83", {
                const res = await fetch("https://run.mocky.io/v3/676d80fc-9ec9-4c38-9323-672fc7de6a9f", {
                    method: 'GET',
                    headers: {
                        "Accept": "application/json"
                    }
                });

                return res.json();
            },
            getFile: function () {
                this.getLogData(this.endpointSelected).then(result => {
                    this.items = result;
                });
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