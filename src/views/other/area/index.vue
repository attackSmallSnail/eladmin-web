<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <el-input v-model="crud.query.areaName" style="width: 300px;" placeholder="查询区域名称" /> <el-button @click="crud.toQuery">查询</el-button>
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-form-item label="区域名称">
            <el-input v-model="form.areaName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="id" prop="areaId">
            <el-input v-model="form.areaId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="父级id">
            <el-input v-model="form.parentId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="规则">
            <el-input v-model="form.urbanRural" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="区域负责人">
            <el-input v-model="form.areaPerson" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="是否使用">
            <el-input v-model="form.inUse" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="区域简称">
            <el-input v-model="form.areaShort" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="区域类型">
            <el-input v-model="form.areaType" style="width: 370px;" />
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button type="text" @click="crud.cancelCU">取消</el-button>
          <el-button :loading="crud.status.cu === 2" type="primary" @click="crud.submitCU">确认</el-button>
        </div>
      </el-dialog>
      <!--表格渲染-->
      <el-table ref="table" v-loading="crud.loading" :data="crud.data" size="small" style="width: 100%;" @selection-change="crud.selectionChangeHandler">
        <el-table-column type="selection" width="55" />
        <el-table-column prop="areaName" label="区域名称" />
        <el-table-column prop="areaId" label="id" />
        <el-table-column prop="parentId" label="父级id" />
        <el-table-column prop="urbanRural" label="规则" />
        <el-table-column prop="areaPerson" label="区域负责人" />
        <el-table-column prop="inUse" label="是否使用" />
        <el-table-column prop="areaShort" label="区域简称" />
        <el-table-column prop="areaType" label="区域类型" />
        <el-table-column v-if="checkPer(['admin','sysAreaFjzl:edit','sysAreaFjzl:del'])" label="操作" width="150px" align="center">
          <template slot-scope="scope">
            <udOperation
              :data="scope.row"
              :permission="permission"
            />
          </template>
        </el-table-column>
      </el-table>
      <!--分页组件-->
      <pagination />
    </div>
  </div>
</template>

<script>
import crudSysAreaFjzl from '@/api/other/sysAreaFjzl'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'

const defaultForm = { areaName: null, areaId: null, parentId: null, urbanRural: null, areaPerson: null, inUse: null, areaShort: null, areaType: null }
export default {
  name: 'SysAreaFjzl',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: '区域编码表,维护数据区域', url: 'api/sysAreaFjzl', idField: 'areaId', sort: 'areaId,asc', crudMethod: { ...crudSysAreaFjzl }})
  },
  data() {
    return {
      permission: {
        add: ['admin', 'sysAreaFjzl:add'],
        edit: ['admin', 'sysAreaFjzl:edit'],
        del: ['admin', 'sysAreaFjzl:del']
      },
      rules: {
        areaId: [
          { required: true, message: 'id不能为空', trigger: 'blur' }
        ]
      }}
  },
  methods: {
    // 钩子：在获取表格数据之前执行，false 则代表不获取数据
    [CRUD.HOOK.beforeRefresh]() {
      return true
    }
  }
}
</script>

<style scoped>

</style>
