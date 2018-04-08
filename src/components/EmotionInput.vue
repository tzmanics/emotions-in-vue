<template>
  <div class="emotion-box">
    <div class="emotion-logging">
      <h2> What are you feeling? </h2>
      <kendo-datepicker
        v-model="emotionDate"
        :min="minDate"
        :max="maxDate"
        :value="emotionDate"
        :format="'MM/dd/yy'"
      >
      </kendo-datepicker>
      <kendo-dropdownlist
        v-model="emotionSelected"
        :data-source="emotionArray"
        :index="0" >
      </kendo-dropdownlist>
      <kendo-button @click='addEmotion'> Add Emotion </kendo-button>
    </div>
    <div class="emotion-graph">
      <h2> The View </h2>
      <kendo-chart
        :series-defaults-type="'pie'"
        :chart-area-background="''"
        :series="series"
        :tooltip="tooltip">
      </kendo-chart>
    </div>
  </div>
</template>

<script>
export default {
  name: 'emotion-input',
  data () {
    return {
      emotionDate: new Date(),
      emotionArray: [
        '😃', '😢', '🤣', '😡'
      ],
      happyFeels: 0,
      sadFeels: 0,
      funnyFeels: 0,
      angryFeels: 0,
      emotionSelected: '😃',
      minDate: new Date(2017, 1, 1),
      maxDate: new Date(),
      tooltip: { visible: true, template: '#= value # day(s)' }
    }
  },
  methods: {
    addEmotion () {
      switch (this.emotionSelected) {
        case '😃':
          this.happyFeels = this.happyFeels + 1
          break
        case '😢':
          this.sadFeels = this.sadFeels + 1
          break
        case '🤣':
          this.funnyFeels = this.funnyFeels + 1
          break
        case '😡':
          this.angryFeels = this.angryFeels + 1
          break
        default:
          console.log('No feels felt 😶')
      }
    }
  },
  computed: {
    series: function () {
      return [{
        data: [{
          category: '😃',
          value: this.happyFeels,
          color: '#BCFF3A'
        }, {
          category: '😢',
          value: this.sadFeels,
          color: '#5A9CE8'
        }, {
          category: '🤣',
          value: this.funnyFeels,
          color: '#E8DC36'
        }, {
          category: '😡',
          value: this.angryFeels,
          color: '#FF3938'
        }]
      }]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .emotion-box {
    background-color: rgba(255, 255, 255, 0.5);
    margin: 0 auto;
    min-width: 600px;
    padding: 15px;
    width: 47%;
  }

  .k-chart {
    width: 90%;
  }
</style>
