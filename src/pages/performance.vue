<script setup>
import performance from '~/apis/performance.json'

const tableData = performance
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
  const msg = `<pre>${row.config}</pre>`
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
  <div text-gray:80>
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
      <el-table-column prop="model" label="Model" />
      <el-table-column prop="fold" label="Fold" />
      <el-table-column prop="auprc" label="AUPRC" />
      <el-table-column prop="auroc" label="AUROC" />
      <el-table-column prop="accuracy" label="ACC" />
      <el-table-column prop="es" label="ES" show-overflow-tooltip />
      <el-table-column prop="mae" label="MAE" />
      <el-table-column prop="mse" label="MSE" />
      <el-table-column prop="rmse" label="RMSE" />
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
