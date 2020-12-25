<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <el-input v-model="crud.query.orgName" style="width: 300px;" placeholder="查询机构名称" />
      <el-input v-model="crud.query.deptName" style="width: 300px;" placeholder="查询部门名称" /> <el-button @click="crud.toQuery">查询</el-button>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-form-item label="科室名称">
            <el-input v-model="form.deptName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构名称">
            <el-input v-model="form.orgName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构id" prop="orgId">
            <el-input v-model="form.orgId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="排序码">
            <el-input v-model="form.sortCode" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="分院">
            <el-input v-model="form.hospitalId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="临床科室分类 1-内科 2-外科 3-妇产 4-儿科 5-中医科 6-ICU  9-其他">
            <el-input v-model="form.deptType2" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="科室代码" prop="deptId">
            <el-input v-model="form.deptId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="是否删除">
            <el-input v-model="form.isDelete" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="科室类型 1-门诊科室 2-住院科室 3-护理病区 9-其他">
            <el-input v-model="form.deptType1" style="width: 370px;" />
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
        <el-table-column prop="deptName" label="科室名称" />
        <el-table-column prop="orgName" label="机构名称" />
        <el-table-column prop="orgId" label="机构id" />
        <el-table-column prop="sortCode" label="排序码" />
        <el-table-column prop="hospitalId" label="分院" />
        <el-table-column prop="deptType2" label="临床科室分类 1-内科 2-外科 3-妇产 4-儿科 5-中医科 6-ICU  9-其他" />
        <el-table-column prop="deptId" label="科室代码" />
        <el-table-column prop="isDelete" label="是否删除" />
        <el-table-column prop="deptType1" label="科室类型 1-门诊科室 2-住院科室 3-护理病区 9-其他" />
        <el-table-column v-if="checkPer(['admin','dept:edit','dept:del'])" label="操作" width="150px" align="center">
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
import crudDept from '@/api/other/dept'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'

const defaultForm = { deptName: null, orgName: null, orgId: null, sortCode: null, hospitalId: null, deptType2: null, deptId: null, isDelete: null, deptType1: null }
export default {
  name: 'Dept',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: '分级查询部门表', url: 'api/deptSys', idField: 'deptId', sort: 'orgId,desc', crudMethod: { ...crudDept }})
  },
  data() {
    return {
      permission: {
        add: ['admin', 'dept:add'],
        edit: ['admin', 'dept:edit'],
        del: ['admin', 'dept:del']
      },
      rules: {
        orgId: [
          { required: true, message: '机构id不能为空', trigger: 'blur' }
        ],
        deptId: [
          { required: true, message: '科室代码不能为空', trigger: 'blur' }
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
