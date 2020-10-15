<script>
// ここでこのコンポーネントで使用するグラフの種類を定義する。今回はドーナツグラフなのでDoughnutとなる。
import { Pie } from 'vue-chartjs'

export default ({
  extends: Pie,
  data() {
    return {
      datas: {
        // 凡例とツールチップに表示するラベル
        labels: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
        // 表示するデータ
        datasets: [
          {
            data: [1, 2, 3, 4, 5, 6, 7],
            backgroundColor: ['#f87979', '#aa4c8f', '#38b48b', '#006e54', '#c1e4e9', '#89c3eb', '#c3d825']
          }
        ]
      },
      options: {
        responsive: true,
        legend: {
          position: 'bottom',
          labels: {
            fontSize: 28,
          }
        },
      
      tooltips: {
        bodyFontSize: 28,
        callbacks: {
          label: function(tooltipItem,data){
            let total = 0
            let indexItem = data.datasets[0].data[tooltipItem.index]
            data.datasets[0].data.forEach(item => {
              total += item
            })
            return Math.round(indexItem / total * 100) + ' %'
            }
          }
        }
      }
    }
  },
  mounted() {
    this.renderChart(this.datas, this.options)
  }
})
</script>