<template>
  <v-app>
    <v-container fluid grid-list-lg text-xs-center>
      <v-layout row wrap fluid>
        <v-flex sm3 xs4 v-for="action in actions" :key="action.id">
          <action
            :action="action"
            :isAdmin="isAdmin"
            v-on:remove="deleteAction"
            v-on:update="updateAction"
            v-on:drag="drag"
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
    data() {
      return {
        isAdmin: true,
        actions: []
      }
    },
    mounted() {

      if (window.BX24) {
        BX24.init(() => {
          this.isAdmin = BX24.isAdmin();
          console.log(BX24.isAdmin());
        });
      }

      this.getActionsBX24()
        .then((data) => {
          this.actions = [];
          data.map((el) => {
            this.actions.push({
              id: el.ID,
              active: (el.PROPERTY_VALUES.active == "false" ? false : true),
              name: el.PROPERTY_VALUES.name,
              describe: el.PROPERTY_VALUES.describe,
              color: el.PROPERTY_VALUES.color,
              subColor: el.PROPERTY_VALUES.subColor,
              url: el.PROPERTY_VALUES.url
            });
          });
          console.log(data);
        })
        .catch((err) => {
          this.actions = require('./Data').default;
          console.log(err);
        });
    },
    methods: {
      deleteAction(id) {
        this.actions.map((action) => {
          if (action.id == id) {
            action.active = false;
            action.name = "";
            action.describe = "";
            action.url = "";
            action.color = "";
            action.subColor = "";
            this.updateActionBX24(action)
              .then((res) => {
                console.log(res);
              })
              .catch((err) => {
                console.log(err);
              });
          }
        })
      },
      updateAction(action) {

        this.updateActionBX24(action)
          .then((res) => {
            console.log(res);
          })
          .catch((err) => {
            console.log(err);
          });

        this.actions.map((el) => {
          if (action.id == el.id) {

            for (var key in action) {
              el[key] = action[key];
            }

            return;
          }
        })
      },
      drag(src) {

        console.log('Притащили ' + src.from + " в " + src.to);

        var idFrom = src.from;
        var idTo = src.to;

        var actionFrom, actionTo;

        for (var i = 0; i < this.actions.length; i++) {

          if (this.actions[i].id == idFrom) {
            actionFrom = this.actions[i];
          }
          if (this.actions[i].id == idTo) {
            actionTo = this.actions[i];
          }

          if (actionFrom && actionTo) {
            break;
          }
        }

        for (var key in actionFrom) {
          if (key != 'id') {
            actionTo[key] = actionFrom[key];
          }
        }

        this.updateActionBX24(actionTo)
          .then((res) => {
            console.log(res);
          })
          .catch((err) => {
            console.log(err);
          });

        actionFrom.active = false;
        actionFrom.name = "";
        actionFrom.describe = "";
        actionFrom.url = "";
        actionFrom.color = "";
        actionFrom.subColor = "";

        this.updateActionBX24(actionFrom)
          .then((res) => {
            console.log(res);
          })
          .catch((err) => {
            console.log(err);
          });
      },
      getActionsBX24() {

        return new Promise((resolve, reject) => {
          if (!window.BX24) {
            reject("BX24 not defined!");
          }
          BX24.callMethod(
            'entity.item.get',
            {
              ENTITY: 'action'
            },
            function (result) {
              resolve(result.answer.result);
            }
          );
        });
      },
      updateActionBX24(action) {

        return new Promise((resolve, reject) => {

          if (!window.BX24) {
            reject("BX24 not defined!");
          }
          BX24.callMethod('entity.item.update', {
              ENTITY: 'action',
              ID: action.id,
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                name: action.name,
                describe: action.describe,
                active: action.active,
                color: action.color,
                subColor: action.subColor,
                url: action.url
              },
              SECTION: 0
            },
            function (result) {
              //console.log(result);
              resolve(result);
            });
        });
      }
    },
    components: {
      action
    }
  }
</script>
