<template>
  <div>
    <p class="text-xs-center" v-if="installing">
      <v-progress-circular indeterminate v-bind:size="70" v-bind:width="7" color="blue"></v-progress-circular>
    </p>
    <p class="text-xs-center">
      {{text}}
    </p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        installing: true,
        text: "Выполняется установка..."
      };
    },
    mounted() {

      if (!window.BX24) {
        this.text = "BX24 не инициализирован";
        this.installing = false;
        return;
      }
      this.install()
        .then(() => {
          this.text = "Установка завершена";
          this.installing = false;
          BX24.installFinish();
        })
        .catch((err) => {
          this.text = err.error_description;
          this.installing = false;
        });
    },
    methods: {
      install() {

        var actions = [
          {
            method: 'entity.add',
            params: {
              ENTITY: 'action',
              NAME: 'Actions',
              ACCESS: {
                AU: 'W'
              }
            }
          },
          {
            method: 'entity.item.property.add',
            params: {
              ENTITY: 'action',
              PROPERTY: 'active',
              NAME: 'Active',
              TYPE: 'N'
            }
          },
          {
            method: 'entity.item.property.add',
            params: {
              ENTITY: 'action',
              PROPERTY: 'name',
              NAME: 'Name',
              TYPE: 'S'
            }
          },
          {
            method: 'entity.item.property.add',
            params: {
              ENTITY: 'action',
              PROPERTY: 'describe',
              NAME: 'Describe',
              TYPE: 'S'
            }
          },
          {
            method: 'entity.item.property.add',
            params: {
              ENTITY: 'action',
              PROPERTY: 'color',
              NAME: 'Color',
              TYPE: 'S'
            }
          },
          {
            method: 'entity.item.property.add',
            params: {
              ENTITY: 'action',
              PROPERTY: 'subColor',
              NAME: 'Sub color',
              TYPE: 'S'
            }
          },
          {
            method: 'entity.item.property.add',
            params: {
              ENTITY: 'action',
              PROPERTY: 'url',
              NAME: 'url',
              TYPE: 'S'
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: true,
                name: "1С Битрикс",
                describe: "Перейти на Битрикс",
                color: "yellow",
                subColor: "",
                url: "https://www.1c-bitrix.ru/"
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: true,
                name: "Закладка 2",
                describe: "Перейти на ...",
                color: "blue",
                subColor: "",
                url: "http://"
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          },
          {
            method: 'entity.item.add',
            params: {
              ENTITY: 'action',
              DATE_ACTIVE_FROM: new Date(),
              DETAIL_PICTURE: '',
              NAME: 'Action',
              PROPERTY_VALUES: {
                active: false,
                name: "",
                describe: "",
                color: "",
                subColor: "",
                url: ""
              },
              SECTION: 0
            }
          }
        ];

        console.log('Начало установки!');

        return new Promise((resolve, reject) => {

          BX24.callBatch(
            actions,
            function (result) {

              var error = false;
              var errors = [];

              for (var i = 0; i < result.length; i++) {
                if (result[i].error()) {
                  error = true;
                  //console.log(result[i].error())
                  //break;
                  errors.push(result[i].error().ex);
                }
              }
              if (!error) {
                this.installing = false;
                this.text = "Установка успешно завершена";
                console.log('Установка завершена');
                resolve();
              } else {
                reject(errors);
              }
            },
            true
          );
        });
      }
    }
  }
</script>

