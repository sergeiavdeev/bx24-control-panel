<template>
  <v-app>
    <v-container fluid grid-list-lg text-xs-center>
      <v-layout row wrap fluid>
        <v-flex sm3 xs4 v-for="action in actions" :key="action.id">
          <action
              :action  ="action"
              :isAdmin ="isAdmin"
              v-on:remove="deleteAction"
              v-on:update="updateAction"
          >
          </action>
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>
</template>

<script>
  import action from './Action';

  export default {
    data () {
      return {
        isAdmin: true,
        actions: []
      }
    },
    methods: {
      deleteAction (id) {
        this.actions.map( (action) => {
          if (action.id == id) {
            action.active = false;
            return;
          }
        })
      },
      updateAction (action) {
        this.actions.map( (el) => {
          if (action.id == el.id) {

            for (var key in action) {
              el[key] = action[key];
            }
            return;
          }
        })
      }
    },
    components: {
      action
    },
    mounted () {
      this.actions = require('./Data').default;
    }
  }



</script>
