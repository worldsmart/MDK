<template>
    <div class="form">
        <v-card class="mx-auto" outlined>
            <v-list-item three-line>
                <v-list-item-content>
                    <v-list-item-title class="headline mb-1">Ftp settings</v-list-item-title>
                    <v-text-field v-model="ftp_settings.name" label="Ftp name" hide-details="auto"></v-text-field>
                    <v-text-field v-model="ftp_settings.host" label="Host" hide-details="auto"></v-text-field>
                    <v-text-field v-model="ftp_settings.port" label="Port" hide-details="auto"></v-text-field>
                    <v-text-field v-model="ftp_settings.user" label="User" hide-details="auto"></v-text-field>
                    <v-text-field v-model="ftp_settings.password" label="Password" hide-details="auto"></v-text-field>
                </v-list-item-content>
            </v-list-item>
            <v-card-actions>
                <v-btn class="mr-4" @click="save">Save</v-btn>
            </v-card-actions>
        </v-card>
    </div>
</template>

<script>

    export default {
        name: 'FtpSettings',
        props: ['ftp_settings'],
        components: {

        },
        data(){
            return{

            }
        },
        methods: {
            save: function () {
                this.$http.put('/api/ftp', this.ftp_settings, {
                    headers: {
                        Authorization: localStorage.getItem('jwt')
                    }
                }).then(() => {
                    document.location.reload(true);
                }, (err) => {
                    console.log(err);
                });
            }
        },
        created: function(){

        }
    }
</script>

<style lang="scss">
    .form{
        margin: 20px 40px;
    }
</style>