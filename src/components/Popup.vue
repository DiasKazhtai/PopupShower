<template>
  <div class="text-center Popup">
    <v-dialog
      v-model="dialog"
      width="500"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="red lighten-2"
          dark
          v-bind="attrs"
          v-on="on"
        >
          узнать о компании
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="headline grey lighten-2">
          Инфорамация о компании
        </v-card-title>

        <v-card-text>
          <div class="Popup__space">
            <span class="Popup__label">Название компании: </span>
            <span class="Popup__value">{{ info.name }}</span>
          </div>
          <span class="Popup__label">Города в которых мы находимся: </span>
          <div class="Popup__grid Popup__space" >
            <div class="Popup__grid-item" v-for="item in info.cities" :key="item">
              <span class="Popup__value">{{ item }}</span>
            </div>
          </div>
          <span class="Popup__label">Информация о продуктах: </span>
          <div class="Popup__space">
            <div>
              <span class="Popup__label">Всего продуктов: </span>
              <span class="Popup__value">{{ info.status.totalProducts }}</span>
            </div>
            <div>
              <span class="Popup__label">Доступно продуктов: </span>
              <span class="Popup__value">{{ info.status.availableProducts }}</span>
            </div>
            <div>
              <span class="Popup__label">Недоступно продуктов: </span>
              <span class="Popup__value">{{ info.status.nonAvailableProducts }}</span>
            </div>
          </div>
          <div class="Popup__space">
            <span class="Popup__label">Последний сеанс: </span>
              <span class="Popup__value">{{ info.status.lastCheckDate }}</span>
          </div>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = false"
          >
            Закрыть
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
  export default {
    mounted () {
      fetch('https://bitbucket.org/ilakhmotkin/front-end-assesment-ru/raw/525e8e2fbee5cd98a80499c400f569e77b4f6ffd/server-response.json')
        .then(response => response.json())
        .then(json => {
          this.info.name = json.name 
          this.info.cities = json.cities
          this.info.status.totalProducts = json.status.totalProducts
          this.info.status.availableProducts = json.status.availableProducts
          this.info.status.nonAvailableProducts = json.status.nonAvailableProducts
          this.info.status.lastCheckDate = json.status.lastCheckDate
        })
    },
    data () {
      return {
        dialog: false,
        info: {
            name: '',
        status: {
          lastCheckDate: '',
          totalProducts: '',
          availableProducts: '',
          nonAvailableProducts: '',
        },
        cities: [
        ]
        }
      }
    },
  }
</script>

<style lang="scss" >
    .Popup {
      &__value, &__label {
        font-weight: bold;
        font-size: 16px;
      }
      
      &__label {
        color: black;
        margin: 10px 0 5px 0;
      }

      &__value {
        font-size: 18px;
      }

      &__space {
        margin-bottom: 10px;
        margin-top: 10px;
      }

      &__grid {
        display: grid;
        grid-template-columns: 50% 50%;
        grid-gap: 5px;

        &-item {
          border: 1px solid #1976d2;
          border-radius: 5px;
          cursor: pointer;

          &:hover {
            color: #1976d2;
          }
        }
      }
    }
</style>