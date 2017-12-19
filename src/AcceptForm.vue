<template>
    <v-layout row wrap justify-top>
        <v-dialog v-model="show" v-on:input="$emit('close')" max-width="220px">
            <v-card>
                <v-card-text>
                    <div class="body-1">Удалить элемент?</div>
                </v-card-text>
                <v-card-actions>
                    <v-btn color="primary" flat @click.stop="$emit('close')">Закрыть</v-btn>
                    <v-btn color="primary" flat @click.stop="$emit('delete')">ОК</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-layout>
</template>

<script>
    export default {
        name: "accept-form",
        data () {
            return {
                show: true
            };
        }
    }
</script>

