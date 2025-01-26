<template>
  <div>
    <div class="table-wrapper">
      <table>
        <thead>
          <tr>
            <th>Título</th>
            <th style="text-align: center;">Fecha de creación</th>
            <th style="text-align: right;">Acción</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="report in reports" :key="report.id">
            <td>{{ report.title }}</td>
            <td style="text-align: center;">{{ report.created_at }}</td>
            <td style="text-align: right;">
              <a :href="report.report_link" download style="color: inherit; text-decoration: none;">
                <span style="text-decoration: underline;">Descargar</span>
                <span> 📥</span>
              </a>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="btn-container">
      <button class="btn-primary" @click="showForm = true">
        Crear reporte
      </button>
    </div>

    <ReportForm v-if="showForm" @close="showForm = false" @report-created="addNewReport" />
  </div>
</template>

<script>
import { ref } from 'vue'
import ReportForm from '@/components/ReportForm.vue'

export default {
  name: 'ReportList',
  components: {
    ReportForm
  },
  setup() {
    const showForm = ref(false)
    const reports = ref([
      { id: 1, title: 'Reporte de usuario 1', created_at: '04/02/2020', report_link: '#' },
      { id: 2, title: 'Reporte de usuario 2', created_at: '08/05/2021', report_link: '#' },
      { id: 3, title: 'Reporte de usuario 3', created_at: '20/08/2021', report_link: '#' },
    ])

    function addNewReport(newRep) {
      reports.value.push(newRep)
    }

    return {
      showForm,
      reports,
      addNewReport
    }
  }
}
</script>
