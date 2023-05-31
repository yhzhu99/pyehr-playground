<script setup>
import performance from '~/apis/performance.json'
import hyperparameters from '~/apis/hyperparameters.json'

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
  let modelName = row.model
  if (row.time_aware === true)
    modelName = `${modelName}-ta`

  const hparam = hyperparametersMap.get(`${modelName}+${row.dataset}+${row.task}`)
  // console.log(hyperparametersMap.value)
  const msg = `<pre>${JSON.stringify(hparam, null, 4)}</pre>`
  ElMessageBox.alert(
    msg,
    'Config Detail',
    {
      dangerouslyUseHTMLString: true,
    },
  )
}
</script>

<template>
  <div h-full text-gray:80>
    <div my-4>
      <a href="/assets/performance.csv" download mx-2>
        <el-button type="primary">
          Download CSV
        </el-button>
      </a>
      <a href="/assets/performance.tex" download mx-2>
        <el-button type="success">
          Download Tex
        </el-button>
      </a>
    </div>

    <el-table
      :data="tableData"
      stripe
      size="small"
      border
      style="width: 100%"
      @row-dblclick="showConfig"
    >
      <el-table-column prop="model" label="Model" show-overflow-tooltip />
      <el-table-column prop="fold" label="Fold" show-overflow-tooltip />
      <el-table-column prop="auprc" label="AUPRC" show-overflow-tooltip />
      <el-table-column prop="auroc" label="AUROC" show-overflow-tooltip />
      <el-table-column prop="accuracy" label="ACC" show-overflow-tooltip />
      <el-table-column prop="es" label="ES" show-overflow-tooltip />
      <el-table-column prop="mae" label="MAE" show-overflow-tooltip />
      <el-table-column prop="mse" label="MSE" show-overflow-tooltip />
      <el-table-column prop="rmse" label="RMSE" show-overflow-tooltip />
      <el-table-column prop="osmae" label="OSMAE" show-overflow-tooltip />
      <el-table-column
        prop="dataset"
        label="Dataset"
        width="100"
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
        width="100"
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

<!-- <style scoped>
.pagination-container {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
</style> -->
