<template>
  <v-layout row wrap justify-top>
    <v-dialog v-model="show" max-width="500px" v-on:input="$emit('close')">
      <v-card>
        <v-card-title>Параметры действия:</v-card-title>
        <v-card-text>
          <v-flex xs12>
            <v-text-field label="Заголовок" required v-model="name"></v-text-field>
          </v-flex>
          <v-flex xs12>
            <v-text-field label="Описание" hint="Введите описание заметки" v-model="describe"></v-text-field>
          </v-flex>
          <v-flex xs12>
            <v-text-field label="URL" v-model="url"></v-text-field>
          </v-flex>
          <v-layout row>
            <v-flex xs6>
              <v-select
                  v-bind:items="colors"
                  v-model="color"
                  label="Цвет"
                  single-line
                  bottom
                  append-icon="format_color_fill"
                  hide-details
                  :color="fullColor"
              ></v-select>
            </v-flex>
            <v-flex xs5>
              <v-select
                  v-bind:items="subColors"
                  v-model="subColor"
                  label="Оттенок"
                  single-line
                  bottom
                  append-icon="format_color_fill"
                  hide-details
                  :color="fullColor"
              ></v-select>
            </v-flex>

            <v-flex xs1 :class="fullColor">

            </v-flex>
          </v-layout>
        </v-card-text>
        <!--<material-picker v-model="colors"></material-picker> -->
        <v-card-actions>
          <v-btn color="primary" flat @click.stop="$emit('close')">Закрыть</v-btn>
          <v-btn color="primary" flat @click.stop="$emit('save', {id: id, name: name, describe: describe, url: url, color: color, subColor: subColor, active: true})">ОК</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-layout>
</template>

<script>
  export default {
    name: "action-form",
    data () {
      return {
        name: this.action.name,
        describe: this.action.describe,
        url: this.action.url,
        id: this.action.id,
        color: this.action.color,
        subColor: this.action.subColor,
        colors: require('./Colors').default.colors,
        subColors: require('./Colors').default.subColors,
        show: true
      }
    },
    props: [
      'action'
    ],
    computed: {
      fullColor: function () {

        var result = this.color;

        if(this.subColor != null) {
          result += ' ' + this.subColor;
        }
        return result;
      }
    }
  }
</script>
