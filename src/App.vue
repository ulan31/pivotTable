<template>
  <div id="app">
    <div class="header">
      <div v-if="countryName[0].length > 0" class="countryName">
        <div class="row">Country Name</div>
        <div v-for="item in countryName[0]">
          <div :style="{width: item.lengthChild > 0 ? item.lengthChild *300 + 'px' : 300 + 'px' }" class="row">{{item.name}}</div>
        </div>
      </div>
      <div v-if="countryName[1].length > 0" class="brandName">
        <div class="row">Brand name</div>
        <div v-for="item in countryName[1]">
          <div class="row">{{item.name}}</div>
        </div>
      </div>
    </div>
    <div class="body">
      <div class="block-1">
        <div v-if="districtRegionName[0].length > 0" :style="{width: districtRegionName[2].length > 0 ? 100 + 'px' : 150 + 'px' }" class="districtName">
          <div class="disReg sub">District Name</div>
          <div v-for="dist in districtRegionName[0]">
            <div v-if="districtRegionName[2].length > 0" :style="{height: dist.lengthChild > 0 ? dist.lengthChild *80 + 'px' : 80 + 'px' }" class="disReg">{{dist.name}}</div>
            <div v-else :style="{height: dist.lengthChild > 0 ? dist.lengthChild *40 + 'px' : 40 + 'px' }" class="disReg">{{dist.name}}</div>
          </div>
        </div>
        <div :style="{width: districtRegionName[2].length > 0 ? 100 + 'px' : 150 + 'px' }" v-if="districtRegionName[1].length > 0" class="regionName">
          <div class="disReg sub">Region Name</div>
          <div v-for="region in districtRegionName[1]">
            <div v-if="districtRegionName[2].length > 0" :style="{height: region.lengthChild > 0 ? region.lengthChild *40 + 'px' : 40 + 'px' }" class="disReg">{{region.name}}</div>
            <div v-else class="disReg">{{region.name}}</div>
          </div>
        </div>
        <div :style="{width: districtRegionName[2].length > 0 ? 100 + 'px' : 150 + 'px' }" v-if="districtRegionName[2].length > 0" class="regionName">
          <div class="disReg">City Name</div>
          <div v-for="city in districtRegionName[2]">
            <div class="disReg">{{city.name}}</div>
          </div>
        </div>
      </div>
      <div class="block-2">
        <div style="height: 40px" class="block-2-row" v-for="row in 1">
          <div style="width: 149px" class="sub block-2-column" v-for="(column, key) in countryName[1].length > 0 ? countryName[1].length *2 : countryName[0].length *2">
            <template v-if="key%2 === 0">
              Sum of Metric 1
            </template>
            <template v-else>
              Sum of Metric 2
            </template>
          </div>
        </div>
        <div style="height: 40px" v-for="(row, keyRow) in districtRegionName[2].length > 0 ? districtRegionName[2].length : districtRegionName[1].length" class="block-2-row">
          <template  v-if="countryName[1].length > 0">
            <div style="width: 149px" v-for="(column, key) in countryName[1].length *2" class="block-2-column">{{measureData[keyRow][key]}}</div>
          </template>
          <template v-else>
            <div  style="width: 149px" v-for="(column, key) in countryName[0].length *2" class="block-2-column">{{measureData[keyRow][key]}}</div>
          </template>
        </div>
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
             "dimensionValue": "Приволжский федеральный округ",
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
      const result = [
        countryName,
        brandName
      ]
      return result
    }
   },
   districtRegionName() {
     if(this.data.dimensionData && this.data.dimensionData.rows) {
       const districtName = [];
       const regionName = [];
       const cityName = [];
       for(let item of this.data.dimensionData.rows) {
         districtName.push({
           'name': item.dimensionValue,
           'lengthChild': item.rowsChild && item.rowsChild.length > 0 ? item.rowsChild.length : 0
         })
         if(item.rowsChild) {
           for(let brand of item.rowsChild) {
             regionName.push({
               'name': brand.dimensionValue,
               'lengthChild': brand.rowsChild && brand.rowsChild.length > 0 ? brand.rowsChild.length : 0
             })
             if(brand.rowsChild) {
               for(let city of brand.rowsChild) {
                 cityName.push({
                   'name': city.dimensionValue
                 })
               }
             }
           }
         }
       }
       const result = [
         districtName,
         regionName,
         cityName
       ]
       return result
     }
   },
   measureData() {
     if(this.data.measuresData[0] && this.data.measuresData[0].measureValues && this.data.measuresData[1] && this.data.measuresData[1].measureValues) {
       const result = []
       const measure1 = this.data.measuresData[0].measureValues
       const measure2 = this.data.measuresData[1].measureValues
       for(let i=0; i < measure1.length; i++) {
         for(let j=0; j< measure1[i].length; j++) {
           result.push(measure1[i][j], measure2[i][j])
         }
       }
       const sum = []
       const row = this.countryName[1].length > 0 ? this.countryName[1].length *2 : this.countryName[0].length *2
       for(let k=0; k < Math.ceil(result.length/row); k++) {
         sum[k] = result.slice((k*row), (k*row) + row)
       }
       return sum
     }
     if(this.data.measuresData[0] && this.data.measuresData[0].measureValues) {
       const result = []
       const measure1 = this.data.measuresData[0].measureValues
       for(let i=0; i < measure1.length; i++) {
         for(let j=0; j< measure1[i].length; j++) {
           result.push(measure1[i][j], '')
         }
       }
       const sum = []
       const row = this.countryName[1].length > 0 ? this.countryName[1].length *2 : this.countryName[0].length *2
       for(let k=0; k < Math.ceil(result.length/row); k++) {
         sum[k] = result.slice((k*row), (k*row) + row)
       }
       return sum
     }
     if(this.data.measuresData[1] && this.data.measuresData[1].measureValues) {
       const result = []
       const measure1 = this.data.measuresData[1].measureValues
       for(let i=0; i < measure1.length; i++) {
         for(let j=0; j< measure1[i].length; j++) {
           result.push(measure1[i][j], '')
         }
       }
       const sum = []
       const row = this.countryName[1].length > 0 ? this.countryName[1].length *2 : this.countryName[0].length *2
       for(let k=0; k < Math.ceil(result.length/row); k++) {
         sum[k] = result.slice((k*row), (k*row) + row)
       }
       return sum
     }
   },
  },
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
  outline: 1px solid black;
  background-color: darkturquoise;
}

/*body*/
.body {
  /*border: 1px solid greenyellow;*/
  display: flex;
  flex-direction: row;
}
.block-1 {
  display: flex;
  flex-direction: row;
}
.districtName {
  display: flex;
  flex-direction: column;
  width: 150px;
}
.regionName {
  display: flex;
  flex-direction: column;
  width: 150px;
}
.disReg {
  outline: 1px solid black;
  height: 40px;
  overflow: hidden;

}

.sub {
  /*background-color: paleturquoise;*/
}

/*measare*/
.block-2 {
  /*display: flex;*/
  /*flex-direction: row;*/
}
.block-2-row {
  display: flex;
  flex-direction: row;
  border-bottom: 1px solid black;
}
.block-2-column {
  display: flex;
  flex-direction: column;
  /*outline: 1px solid darkblue;*/
  border-right: 1px solid black;
  text-align: center;
  font-weight: bold;
}


</style>
