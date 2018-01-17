<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm_8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Http</h1>
                <div class="form-group">
                    <label>Username</label>
                    <input type="text" class="form-control" v-model="user.username">
                </div>
                <div class="form-group">
                    <label>Mail</label>
                    <input type="text" class="form-control" v-model="user.email">
                </div>
                <button class="btn btn-primary" @click="submit">
                    Submit
                </button>
                <hr>
                <input type="text" class="form-control" v-model="node">
                <br><br>
                <button class="btn btn-primary" @click="fetchData">Get Data
                </button>
                <ul class="list-group">
                    <li class="list-group-item" v-for="user in users" >{{ user.username }} - {{ user.email }}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                user: {
                    username: '',
                    email: ''
                },
                users: [],
                resource: {},
                node: 'data'
            }
        },
        methods: {
            submit() {
//                this.$http.post('data.json', this.user)
//                    .then((response) => {
//                        console.log('response', response);
//                    }, (error) =>  {
//                        console.log('error', error)
//                    })
//                this.resource.save({}, this.user);
                this.resource.saveAlt(this.user)
            },
            fetchData() {
//                this.$http.get('data.json')
//                    .then((response) => {
//                        return response.json();
//                    },
//                        (error) => {
//                            console.log('error', error)
//                        }
//                    )
//                    .then((response) => {
//                        Object.keys(response).forEach((e) => this.users.push(response[e]));;
//                    })
//                this.resource.getData({node: this.node, another: 'dede'}).then((response) => {
                this.resource.getData({node: this.node}).then((response) => {
                        return response.json();
                    },
                        (error) => {
                            console.log('error', error)
                        }
                    )
                    .then((response) => {
                        Object.keys(response).forEach((e) => this.users.push(response[e]));;
                    });
            }
        },
        created() {
            const customActions = {
                saveAlt: { method: 'POST', url: 'alternative.json' },
                getData: { method: 'GET'}
            };
//            this.resource = this.$resource('data.json', {}, customActions);
//            this.resource = this.$resource('{node}/{another}.json', {}, customActions);
            this.resource = this.$resource('{node}.json', {}, customActions);
        }

    }
</script>

<style>

</style>
