<template>
  <v-card tile hover @click.native.stop="click()" height="180px" :color="action.color + ' ' + action.subColor" v-if="action.active" draggable="true" @dragstart="dragStart($event)">
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
  <v-card v-else-if="!action.active&&isAdmin" height="180px" flat hover @click.native.stop="openEdit()" @dragend="dragEnd($event)" @drop="drop($event)" @dragover = "dragOver($event)">
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

        var url = this.action.url;

        if (url == undefined) {
          return;
        }

        if ("" + url.length > 0) {
          window.open(url, '_blank');
        }
      },
      closeEdit () {
        this.edit = false;
      },
      update (action) {

        this.$emit('update', action);
        this.edit = false;
      },
      dragStart (e) {

        e.dataTransfer.setData("text", this.action.id);
        e.dataTransfer.effectAllowed="move";
        e.dataTransfer.dropEffect = "move";

        return true;
      },
      dragOver (e) {

        e.dataTransfer.dropEffect="move"
        e.returnValue=false;
        return true;
      },
      drop (e) {

        var id = e.dataTransfer.getData("text");
        this.$emit('drag', {from: id, to: this.action.id});
        return true;
      },
      dragEnd (e) {

      }
    },
    components: {
      actionForm
    }
  }
</script>
