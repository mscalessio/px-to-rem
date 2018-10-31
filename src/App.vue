<template>
  <div id="app" class="page-container">
    <md-app>
      <md-app-toolbar class="md-primary">
        <span class="md-title">PX2REM</span>
      </md-app-toolbar>
      <md-app-content>
        <div class="md-layout md-gutter md-alignment-top-left">
          <md-card class="md-layout-item md-small-size-100">
            <md-card-header>
              <div class="md-title">Converter</div>
            </md-card-header>
            <md-card-content>
              <md-field>
                <label for="default-size">Default Size</label>
                <md-input type="number" id="default-size" name="default-size" v-model="defaultSize" />
              </md-field>
              <div class="md-layout md-gutter">
                <div class="md-layout-item">
                  <md-field>
                    <label for="unit-px">PX</label>
                    <md-input type="number" id="unit-px" name="unit-px" v-model="unitPx" />
                  </md-field>
                </div>
                <div class="md-layout-item">
                  <md-field>
                    <label for="unit-rem">Rem</label>
                    <md-input type="number" id="unit-rem" name="unit-rem" v-model="unitRem" />
                  </md-field>
                </div>
              </div>
            </md-card-content>
          </md-card>
          <md-table md-card class="md-layout-item md-small-size-100">
            <md-table-toolbar>
              <h1 class="md-title">4 Grid Table</h1>
            </md-table-toolbar>

            <md-table-row>
              <md-table-head class="table-fixed">x</md-table-head>
              <md-table-head class="table-fixed">PX</md-table-head>
              <md-table-head class="table-fixed">Rem</md-table-head>
            </md-table-row>

            <md-table-row v-for="n in 30" :key="n">
              <md-table-cell class="table-fixed">x{{n}}</md-table-cell>
              <md-table-cell class="table-fixed">{{ n * 4 }}</md-table-cell>
              <md-table-cell class="table-fixed">{{ round((n * 4) / defaultSize) }}</md-table-cell>
            </md-table-row>
          </md-table>
        </div>
      </md-app-content>
    </md-app>
  </div>
</template>

<script>

const DECIMAL_PRECISION = 2
function round (n, precision = DECIMAL_PRECISION) {
  return Math.round(n * Math.pow(10, precision)) / Math.pow(10, precision)
}

export default {
  name: 'App',
  components: {},
  data () {
    return {
      defaultSize: 16,
      unitPx: 16,
      unitRem: 1
    }
  },
  methods: {
    round
  },
  watch: {
    defaultSize: function (val) {
      this.unitRem = round(this.unitPx / val)
    },
    unitPx: function (val) {
      this.unitRem = round(val / this.defaultSize)
    },
    unitRem: function (val) {
      this.unitPx = round(val * this.defaultSize)
    }
  }
}
</script>

<style>
.table-fixed {
  width: 20px;
  height: auto;
}
</style>
