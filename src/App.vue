<template>
  <div id="app">
    <div class="header">
      <div class="countryName">
        <div  class="row">Country Name</div>
        <template v-if="countryName[0]">
          <div v-for="item in countryName[0]">
            <div :style="{width: item.lengthChild > 0 ? item.lengthChild *300 + 'px' : 300 + 'px' }" class="row">{{item.name}}</div>
          </div>
        </template>
      </div>
      <div v-if="countryName[1].length > 0" class="brandName">
        <div class="row">Brand name</div>
        <template>
          <div v-for="item in countryName[1]">
            <div class="row">{{item.name}}</div>
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
     data: {
       "columnsMeta": [
         {
           "dimensionId": 0,
           "name": "Country name",
           "aliasName": "",
           "type": "string",
           "hierarchy": null
         },
         {
           "dimensionId": 1,
           "name": "Brand name",
           "aliasName": "",
           "type": "string",
           "hierarchy": null
         }
       ],
       "rowsMeta": [
         {
           "dimensionId": 0,
           "name": "District name",
           "aliasName": "",
           "type": "string",
           "hierarchy": null
         },
         {
           "dimensionId": 1,
           "name": "Region name",
           "aliasName": "",
           "type": "string",
           "hierarchy": null
         }
       ],
       "measureMetas": [
         {
           "measureId": 0,
           "name": "Metric 1",
           "alias": "",
           "aggType": "sum",
           "type": "number"
         },
         {
           "measureId": 1,
           "name": "Metric 2",
           "alias": "",
           "aggType": "sum",
           "type": "number"
         }
       ],
       "dimensionData": {
         "columnsLevelCount": 2,
         "rowsLevelCount": 2,
         "columnsCount": 3,
         "rowsCount": 4,
         "columns": [
           {
             "dimensionId": 0,
             "coordinate": 0,
             "dimensionValue": "Италия",
             "columnsChild":[
               {
                 "dimensionId": 1,
                 "coordinate": 0,
                 "dimensionValue": "Бренд 2",
                 "columnsChild": null
               }
             ]
           },
           {
             "dimensionId": 0,
             "coordinate": 1,
             "dimensionValue": "Россия",
             "columnsChild":[
               {
                 "dimensionId": 1,
                 "coordinate": 0,
                 "dimensionValue": "Бренд 1",
                 "columnsChild": null
               },
               {
                 "dimensionId": 1,
                 "coordinate": 1,
                 "dimensionValue": "Бренд 3",
                 "columnsChild": null
               }
             ]
           }
         ],
         "rows": [
           {
             "dimensionId": 0,
             "coordinate": 0,
             "dimensionValue": "Дальневосточный федеральный округ",
             "rowsChild": [
               {
                 "dimensionId": 1,
                 "coordinate": 0,
                 "dimensionValue": "Амурская область",
                 "rowsChild": null
               },
               {
                 "dimensionId": 1,
                 "coordinate": 1,
                 "dimensionValue": "Еврейская область",
                 "rowsChild": null
               }
             ]
           },
           {
             "dimensionId": 0,
             "coordinate": 1,
             "dimensionValues": "Приволжский федеральный округ",
             "rowsChild": [
               {
                 "dimensionId": 1,
                 "coordinate": 0,
                 "dimensionValue": "Кировская область",
                 "rowsChild": null
               },
               {
                 "dimensionId": 1,
                 "coordinate": 1,
                 "dimensionValue": "Нижегордская область",
                 "rowsChild": null
               }
             ]
           }
         ]
       },
       "measuresData": [
         {
           "measureId": 0,
           "measureValues": [
             [
               3,
               8,
               9
             ],
             [
               5,
               6,
               8
             ],
             [
               15,
               16,
               18
             ],
             [
               19,
               20,
               21
             ]
           ]
         },
         {
           "measureId": 1,
           "measureValues": [
             [
               30,
               40,
               50
             ],
             [
               60,
               70,
               80
             ],
             [
               90,
               140,
               150
             ],
             [
               160,
               170,
               180
             ]
           ]
         }
       ]
     }
    }
  },
  computed: {
   countryName() {
    if(this.data.dimensionData && this.data.dimensionData.columns) {
      const countryName = [];
      const brandName = [];
      for(let item of this.data.dimensionData.columns) {
        countryName.push({
          'name': item.dimensionValue,
          'lengthChild': item.columnsChild && item.columnsChild.length > 0 ? item.columnsChild.length : 0
        })
        if(item.columnsChild) {
          for(let brand of item.columnsChild) {
            brandName.push({
              'name': brand.dimensionValue,

            })
          }
        }
      }
      console.log(countryName)
      console.log(brandName)
      const result = [
        countryName,
        brandName
      ]
      return result
    }
   }
  },
  methods: {

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.header {
  /*border: 1px solid black;*/
  display: flex;
  flex-direction: column;
}
.countryName {
  /*border: 1px solid green;*/
  display: flex;
  flex-direction: row;
}
.brandName {
  /*border: 1px solid paleturquoise;*/
  display: flex;
  flex-direction: row;
}
.row {
  width: 300px;
  text-align: center;
  border: 1px solid black;
}
</style>
