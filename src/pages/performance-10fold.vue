<script setup>
import { Download } from '@element-plus/icons-vue'

import performance from '~/apis/performance_10fold.json'
import hyperparameters from '~/apis/hyperparameters.json'

const router = useRouter()

const tableData = performance
const hyperparametersMap = new Map()

hyperparameters.forEach((item) => {
  let modelName = item.model
  if (item.time_aware === true)
    modelName = `${modelName}-ta`

  hyperparametersMap.set(`${modelName}+${item.dataset}+${item.task}`, item)
})

// const currentPage = ref(1)
// const pageSize = ref(10)
// const totalItems = ref(tableData.length)
// function handleCurrentChange(page) {
//   currentPage.value = page
// }
// function handleSizeChange(size) {
//   pageSize.value = size
// }

function filterModel(value, row) {
  return row.model === value
}

function filterTask(value, row) {
  return row.task === value
}

function taskTagColor(value) {
  if (value === 'outcome')
    return 'success'

  else if (value === 'los')
    return 'danger'

  else if (value === 'multitask')
    return 'info'

  else if (value === 'twostage')
    return 'warning'
}

function filterDataset(value, row) {
  return row.dataset === value
}

function showConfig(row, column, event) {
  const hparam = hyperparametersMap.get(`${row.model}+${row.dataset}+${row.task}`)
  // console.log(hyperparametersMap.value)
  const msg = `<pre>${JSON.stringify(hparam, null, 4)}</pre>`
  ElMessageBox.alert(
    msg,
    'Configuration Detail',
    {
      dangerouslyUseHTMLString: true,
    },
  )
}

function onBack() {
  router.push('/')
}
</script>

<template>
  <div h-full text-gray:80>
    <div my-4>
      <el-page-header :icon="null" @back="onBack">
        <template #content>
          <div class="flex items-center">
            <span class="text-large mr-3 font-600"> Performance Table </span>
            <el-tag mr-3>
              10-Fold
            </el-tag>
            <div text-sm>
              Double-click the row to see the hyperparameters.
            </div>
          </div>
        </template>
        <template #extra>
          <div class="flex items-center">
            <a href="/assets/performance.csv" download mx-2>
              <el-button :icon="Download">
                Download CSV
              </el-button>
            </a>
            <a href="/assets/performance.tex" download mx-2>
              <el-button :icon="Download">
                Download Tex
              </el-button>
            </a>
          </div>
        </template>
      </el-page-header>
    </div>
    <div class="banner">
      To submit your scores to the leaderboard or engage with the benchmark, please reach out to us at
      <a href="mailto:yhzhu99@gmail.com"> yhzhu99@gmail.com </a>.
      <br>
      We'll promptly review your solutions and update the leaderboard accordingly.
    </div>
    <el-table
      :data="tableData"
      stripe
      size="small"
      border
      class="table"
      @row-dblclick="showConfig"
    >
      <el-table-column
        prop="model"
        label="Model"
        width="100"
        :filters="
          [
            { text: 'DT', value: 'DT' },
            { text: 'RF', value: 'RF' },
            { text: 'GBDT', value: 'GBDT' },
            { text: 'XGBoost', value: 'XGBoost' },
            { text: 'CatBoost', value: 'CatBoost' },
            { text: 'MLP', value: 'MLP' },
            { text: 'GRU', value: 'GRU' },
            { text: 'RNN', value: 'RNN' },
            { text: 'LSTM', value: 'LSTM' },
            { text: 'TCN', value: 'TCN' },
            { text: 'Transformer', value: 'Transformer' },
            { text: 'AdaCare', value: 'AdaCare' },
            { text: 'Agent', value: 'Agent' },
            { text: 'StageNet', value: 'StageNet' },
            { text: 'RETAIN', value: 'RETAIN' },
            { text: 'GRASP', value: 'GRASP' },
            { text: 'MCGRU', value: 'MCGRU' },
            { text: 'MLP-ta', value: 'MLP-ta' },
            { text: 'GRU-ta', value: 'GRU-ta' },
            { text: 'RNN-ta', value: 'RNN-ta' },
            { text: 'LSTM-ta', value: 'LSTM-ta' },
            { text: 'TCN-ta', value: 'TCN-ta' },
            { text: 'Transformer-ta', value: 'Transformer-ta' },
            { text: 'AdaCare-ta', value: 'AdaCare-ta' },
            { text: 'Agent-ta', value: 'Agent-ta' },
            { text: 'StageNet-ta', value: 'StageNet-ta' },
            { text: 'RETAIN-ta', value: 'RETAIN-ta' },
            { text: 'GRASP-ta', value: 'GRASP-ta' },
            { text: 'MCGRU-ta', value: 'MCGRU-ta' },
          ]"
        :filter-method="filterModel"
        filter-placement="bottom-end"
      />
      <el-table-column prop="auprc" label="AUPRC" show-overflow-tooltip sortable />
      <el-table-column prop="auroc" label="AUROC" show-overflow-tooltip sortable />
      <el-table-column prop="accuracy" label="ACC" show-overflow-tooltip sortable />
      <el-table-column prop="es" label="ES" show-overflow-tooltip sortable />
      <el-table-column prop="mae" label="MAE" show-overflow-tooltip sortable />
      <el-table-column prop="mse" label="MSE" show-overflow-tooltip sortable />
      <el-table-column prop="osmae" label="OSMAE" show-overflow-tooltip sortable />
      <el-table-column
        prop="dataset"
        label="Dataset"
        :filters="[
          { text: 'tjh', value: 'tjh' },
          { text: 'cdsl', value: 'cdsl' },
        ]"
        :filter-method="filterDataset"
        filter-placement="bottom-end"
      >
        <template #default="scope">
          <el-tag
            :type="scope.row.dataset === 'cdsl' ? '' : 'success'"
            disable-transitions
          >
            {{ scope.row.dataset }}
          </el-tag>
        </template>
      </el-table-column>

      <el-table-column
        prop="task"
        label="Task"
        width="90"
        :filters="[
          { text: 'outcome', value: 'outcome' },
          { text: 'los', value: 'los' },
          { text: 'multitask', value: 'multitask' },
          { text: 'twostage', value: 'twostage' },
        ]"
        :filter-method="filterTask"
        filter-placement="bottom-end"
      >
        <template #default="scope">
          <el-tag
            :type="taskTagColor(scope.row.task)"
            disable-transitions
          >
            {{ scope.row.task }}
          </el-tag>
        </template>
      </el-table-column>
    </el-table>

    <!-- <div class="pagination-container">
      <el-pagination
        v-model:current-page="currentPage"
        :page-sizes="[10, 15, 20, 30, 40]"
        :page-size="pageSize"
        :total="totalItems"
        layout="total, sizes, prev, pager, next, jumper"
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
      />
    </div> -->
  </div>
</template>

<style scoped>
/* .pagination-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
} */
.table {
  width: 100%;
  margin-top: 20px;
}
</style>
