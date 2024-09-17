<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  // props: ['CO2Array', 'PM25Array', 'XAxis'],
  data: () => ({
    chartdata: {
      labels: [1,2,3,4,5],
      datasets: [
        {
          label: 'CO2',
          backgroundColor: '#fa0',
          borderColor: '#fa0',
          data: [10,40,50,60,57],
          fill: false,
          yAxisID: 'chart_co2',
          lineTension: 0, // 設置為0以禁用曲線
        }
      ]
    },
    options: {
      responsive: true, // 預設true
      maintainAspectRatio: false, // 預設false
      tooltips: { // hover 顯示的設定
        backgroundColor: '#33333390',
        titleFontSize: 20,
        bodyFontSize: 20
      },
      title:{
        display: false,
        text: '標題標題',
        fontColor: '#fff',
        fontSize: 40,
        position: 'bottom',
      },
      legend: { //標籤
        display: false,
        position: 'top',
        align: 'end',
        labels: {
          fontColor: '#fff',
          fontSize: 24,
        }
      },
      scales : {
        yAxes:[
          {
            id: 'chart_co2',
            // type: 'linear',
            ticks: {
              fontColor: '#333',
              fontSize: '18',
              beginAtZero: true, // 從0開始
              // fixedStepSize: 10 // 設置固定的步長
              display: true,
            },
            gridLines: {
              display: true,
              color: '#aaaaaa80'
            },
            scaleLabel: {
              display: false,
              labelString: 'CO2',
              fontColor: '#fa0',
              fontSize: 20
            },
            position: 'left',
          }
        ],
        xAxes:[
          {
            ticks: { // x軸文字
              fontColor: "#333",
              fontSize: 18,
              // autoSkip: true,
              // maxTicksLimit: 10 // x軸總共秀幾個item
            },
            gridLines: { //x軸網格線
              display: false,
              color: "#888"
            },
            scaleLabel: {
              display: false,
              labelString: '時間',
              fontColor: '#fff',
              fontSize: 20
            },
          }
        ],
      },
    },
  }),

  mounted () {
    this.renderChart(this.chartdata, this.options)
  },
  computed: {},
  methods: {},
}
</script>

<style lang="scss" scoped>
</style>