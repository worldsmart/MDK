<template>
    <div class="table">
        <v-text-field v-model="search_string" @input="search" label="Search"></v-text-field>
        <v-simple-table dense>
            <template v-slot:default>
                <thead>
                <tr>
                    <th class="text-left">ID</th>
                    <th class="text-left">Name</th>
                    <th class="text-left">Date</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="item in display_orders" :key="item.id" @click="goToOrder(item.id)">
                    <td>{{ item.id }}</td>
                    <td>{{ item.name }}</td>
                    <td>{{ item.date }}</td>
                </tr>
                </tbody>
            </template>
        </v-simple-table>
    </div>
</template>

<script>
    export default {
        name: 'OrderList',
        props: ['orders'],
        data(){
            return{
                display_orders: this.orders
            }
        },
        methods: {
            search(){
                this.display_orders = this.orders.filter((customer)=>{
                    return !customer.name.indexOf(this.search_string);
                });
            },
            goToOrder(id){
                this.$router.push({ path: '/order', query: { id: id } });
            }
        },
        created: function(){

        }
    }
</script>

<style lang="scss">
    .table{
        margin: 10px 20px;
    }
</style>