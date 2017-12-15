<template>
  <v-card tile hover @click.native.stop="click()" height="180px" :color="action.color + ' ' + action.subColor" v-if="action.active" class="drag">
    <v-card-actions :class="action.color + ' ' + action.subColor">
      <div class="title">{{action.name}}</div>
      <v-spacer></v-spacer>
      <v-btn icon @click.stop="$emit('remove', action.id)"  v-show="isAdmin" >
        <v-icon>clear</v-icon>
      </v-btn>
      <v-btn icon @click.stop="openEdit()"  v-show="isAdmin" >
        <v-icon>create</v-icon>
      </v-btn>
    </v-card-actions>
    <v-card-text @click.native.stop="cardClick">
      <div class="body-1">{{action.describe}}</div>
    </v-card-text>
    <action-form v-if="edit" :action="action" v-on:close="edit = false" v-on:save="update"></action-form>
  </v-card>
  <v-card v-else-if="!action.active&&isAdmin" height="180px" flat hover @click.native.stop="openEdit()">
    <v-card-text>
      <div class="body-1">
        <v-icon x-large>settings</v-icon>
      </div>
    </v-card-text>
    <action-form v-if="edit" :action="action" v-on:close="edit = false" v-on:save="update"></action-form>
  </v-card>
</template>

<script>

  import actionForm from './ActionForm';

  export default {
    data () {
      return {
        edit: false
      }
    },
    props: [
      'action',
      'isAdmin'
    ],
    methods: {
      openEdit () {
        this.edit = true;
      },
      click () {
        var url = "" + this.action.url;

        if (url.length > 0) {
          window.open(url, '_blank');
        }
      },
      closeEdit () {
        this.edit = false;
      },
      update (action) {

        this.$emit('update', action);
        this.edit = false;
      }
    },
    components: {
      actionForm
    }
  }
</script>
