<template>
  <div id="app">
    <h1>PDF Export</h1>
    <div class="export_container" id="export_container">
      <div class="value_container">
        <h3>日期： {{ getYMD() }}</h3>
        <h3>耗電量： {{ '272 kWh' }}</h3>
      </div>
      <div class="chart_container">
        <SampleChart class="my-chart"/>
      </div>
      <p>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Hic dolore sit laboriosam consequuntur accusantium? Maxime facere eos alias officiis rem ipsa similique inventore facilis asperiores ab, rerum eius, modi vero? Ut, beatae nam? Incidunt, harum eligendi, numquam magnam vero optio ea voluptatibus libero ipsam a, reiciendis dolorem dignissimos quam quas? Iusto odit veritatis illum praesentium fugit dolorem eius ipsa, ducimus ullam quae aliquam officia, hic dignissimos obcaecati quo omnis laboriosam reprehenderit suscipit, neque voluptatum iste harum non amet. Reiciendis tenetur a odio officia unde ipsa atque, beatae perferendis.</p>
    </div>
    
    <button class="export_btn" @click="exportPDF()">輸出</button>
  </div>
</template>

<script>
import SampleChart from './components/SampleChart.vue';
import html2canvas from 'html2canvas';
import jsPDF from 'jspdf';

export default {
  name: 'App',
  components: { SampleChart},
  methods: {
    exportPDF() {
      const el = document.getElementById('export_container');
      // const el = document.querySelector('.export_container');
      html2canvas(el).then((canvas) => {
        const imgData = canvas.toDataURL('image/png');
        const pdf = new jsPDF();
        pdf.addImage(imgData, 'PNG', 0, 0);
        pdf.save('test.pdf');
      });
    },
    getYMD() {
      const date = new Date();
      const yy = date.getFullYear();
      const mm = date.getMonth() + 1;
      const dd = date.getDate();
      return `${yy}/${mm}/${dd}`
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1{
  margin-bottom: 3rem;
}

.export_container{
  width: 770px;
  /* !!!寬度會影響到PDF輸出 */
  margin: 0 auto;
}

.value_container{
  width: 70%;
  margin: 0 auto ;
  display: flex;
  justify-content: center;

  h3{
    margin: 2rem;
  }
}

.chart_container{
  width: 90%;
  margin: 0 auto 3rem;
  /* border: 1px solid #f00; */
  
  .my-chart{
    height: 500px;
  }
}

button.export_btn{
  font-size: 20px;
  padding: .5rem 1.5rem;
}


</style>
