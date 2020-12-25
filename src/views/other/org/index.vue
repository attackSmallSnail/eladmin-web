<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <el-input
        v-model="crud.query.orgName"
        style="width: 300px;"
        placeholder="查询机构名称"
      /> <el-button @click="crud.toQuery">查询</el-button>
      <!--如果想在工具栏加入更多按钮，可以使用插槽方式， slot = 'left' or 'right'-->
      <crudOperation :permission="permission" />
      <!--表单组件-->
      <el-dialog :close-on-click-modal="false" :before-close="crud.cancelCU" :visible.sync="crud.status.cu > 0" :title="crud.status.title" width="500px">
        <el-form ref="form" :model="form" :rules="rules" size="small" label-width="80px">
          <el-form-item label="是否删除">
            <el-input v-model="form.isDelete" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="社保机构代码">
            <el-input v-model="form.socialOrgCode" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构代码">
            <el-input v-model="form.orgCode" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构级别">
            <el-input v-model="form.orgPostlevel" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构id" prop="orgId">
            <el-input v-model="form.orgId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="区域id">
            <el-input v-model="form.areaId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="单位地址 地市">
            <el-input v-model="form.addressCity" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="是否全市机构">
            <el-input v-model="form.ifqsjg" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构性质">
            <el-input v-model="form.orgProperty" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="数据接入状态">
            <el-input v-model="form.connectStatus" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="新农合机构代码">
            <el-input v-model="form.ruralOrgCode" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="创建时间">
            <el-input v-model="form.createDate" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="是否公立机构">
            <el-input v-model="form.ifgljg" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="联系人">
            <el-input v-model="form.linkman" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="是否改革">
            <el-input v-model="form.ifgg00" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="父机构id">
            <el-input v-model="form.parentId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构地址">
            <el-input v-model="form.address" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="是否全市所有基层医疗机构">
            <el-input v-model="form.ifqsjc" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="卫健委机构id">
            <el-input v-model="form.orgIdWjw" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="单位地址 省">
            <el-input v-model="form.addressProvince" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构等级">
            <el-input v-model="form.orgLevel" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构简称">
            <el-input v-model="form.shortName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="电话">
            <el-input v-model="form.tel" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="1已经接入 0未接入">
            <el-input v-model="form.inFlag" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="职工医保机构代码">
            <el-input v-model="form.staffOrgCode" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构描述">
            <el-input v-model="form.orgDesc" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构编号">
            <el-input v-model="form.sid" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="妇幼机构ID">
            <el-input v-model="form.orgIdFy" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="医院类型">
            <el-input v-model="form.orgCategory" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="在同一级机构中的序号">
            <el-input v-model="form.orderNo" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="是否专科机构">
            <el-input v-model="form.ifzkjg" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构类型">
            <el-input v-model="form.orgType" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构等级">
            <el-input v-model="form.orgGrade" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="医院等次">
            <el-input v-model="form.hosOrder" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构名称">
            <el-input v-model="form.orgName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="属于区县的id">
            <el-input v-model="form.belongCountyId" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构对应数据库用户">
            <el-input v-model="form.orgDbUser" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构类别,1机构,2部门">
            <el-input v-model="form.orgkind" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="居民健康档案机构id">
            <el-input v-model="form.jmjkdaOrgid" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="区域名称">
            <el-input v-model="form.areaName" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="公卫机构id">
            <el-input v-model="form.orgIdGw" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="疾控中心机构id">
            <el-input v-model="form.orgIdJkzx" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构负责人">
            <el-input v-model="form.principal" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="单位地址 区县">
            <el-input v-model="form.addressCounty" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="开业时间">
            <el-input v-model="form.foundingTime" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="分管负责人">
            <el-input v-model="form.chargeOfficer" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="机构对应数据库表空间名称">
            <el-input v-model="form.orgDbTablespace" style="width: 370px;" />
          </el-form-item>
          <el-form-item label="邮编">
            <el-input v-model="form.zipCode" style="width: 370px;" />
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
        <el-table-column prop="orgId" label="机构id" />
        <el-table-column prop="orgName" label="机构名称" />
        <el-table-column prop="areaId" label="区域id" />
        <el-table-column prop="isDelete" label="是否删除" />
        <el-table-column prop="socialOrgCode" label="社保机构代码" />
        <el-table-column prop="orgCode" label="机构代码" />
        <el-table-column prop="orgPostlevel" label="机构级别" />
        <el-table-column prop="addressCity" label="单位地址 地市" />
        <el-table-column prop="ifqsjg" label="是否全市机构" />
        <el-table-column prop="orgProperty" label="机构性质" />
        <el-table-column prop="connectStatus" label="数据接入状态" />
        <el-table-column prop="ruralOrgCode" label="新农合机构代码" />
        <el-table-column prop="createDate" label="创建时间" />
        <el-table-column prop="ifgljg" label="是否公立机构" />
        <el-table-column prop="linkman" label="联系人" />
        <el-table-column prop="ifgg00" label="是否改革" />
        <el-table-column prop="parentId" label="父机构id" />
        <el-table-column prop="address" label="机构地址" />
        <el-table-column prop="ifqsjc" label="是否全市所有基层医疗机构" />
        <el-table-column prop="orgIdWjw" label="卫健委机构id" />
        <el-table-column prop="addressProvince" label="单位地址 省" />
        <el-table-column prop="orgLevel" label="机构等级" />
        <el-table-column prop="shortName" label="机构简称" />
        <el-table-column prop="tel" label="电话" />
        <el-table-column prop="inFlag" label="1已经接入 0未接入" />
        <el-table-column prop="staffOrgCode" label="职工医保机构代码" />
        <el-table-column prop="orgDesc" label="机构描述" />
        <el-table-column prop="sid" label="机构编号" />
        <el-table-column prop="orgIdFy" label="妇幼机构ID" />
        <el-table-column prop="orgCategory" label="医院类型" />
        <el-table-column prop="orderNo" label="在同一级机构中的序号" />
        <el-table-column prop="ifzkjg" label="是否专科机构" />
        <el-table-column prop="orgType" label="机构类型" />
        <el-table-column prop="orgGrade" label="机构等级" />
        <el-table-column prop="hosOrder" label="医院等次" />
        <el-table-column prop="belongCountyId" label="属于区县的id" />
        <el-table-column prop="orgDbUser" label="机构对应数据库用户" />
        <el-table-column prop="orgkind" label="机构类别,1机构,2部门" />
        <el-table-column prop="jmjkdaOrgid" label="居民健康档案机构id" />
        <el-table-column prop="areaName" label="区域名称" />
        <el-table-column prop="orgIdGw" label="公卫机构id" />
        <el-table-column prop="orgIdJkzx" label="疾控中心机构id" />
        <el-table-column prop="principal" label="机构负责人" />
        <el-table-column prop="addressCounty" label="单位地址 区县" />
        <el-table-column prop="foundingTime" label="开业时间" />
        <el-table-column prop="chargeOfficer" label="分管负责人" />
        <el-table-column prop="orgDbTablespace" label="机构对应数据库表空间名称" />
        <el-table-column prop="zipCode" label="邮编" />
        <el-table-column v-if="checkPer(['admin','sysOrg:edit','sysOrg:del'])" label="操作" width="150px" align="center">
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
import crudSysOrg from '@/api/other/sysOrg'
import CRUD, { presenter, header, form, crud } from '@crud/crud'
import rrOperation from '@crud/RR.operation'
import crudOperation from '@crud/CRUD.operation'
import udOperation from '@crud/UD.operation'
import pagination from '@crud/Pagination'

const defaultForm = { isDelete: null, socialOrgCode: null, orgCode: null, orgPostlevel: null, orgId: null, areaId: null, addressCity: null, ifqsjg: null, orgProperty: null, connectStatus: null, ruralOrgCode: null, createDate: null, ifgljg: null, linkman: null, ifgg00: null, parentId: null, address: null, ifqsjc: null, orgIdWjw: null, addressProvince: null, orgLevel: null, shortName: null, tel: null, inFlag: null, staffOrgCode: null, orgDesc: null, sid: null, orgIdFy: null, orgCategory: null, orderNo: null, ifzkjg: null, orgType: null, orgGrade: null, hosOrder: null, orgName: null, belongCountyId: null, orgDbUser: null, orgkind: null, jmjkdaOrgid: null, areaName: null, orgIdGw: null, orgIdJkzx: null, principal: null, addressCounty: null, foundingTime: null, chargeOfficer: null, orgDbTablespace: null, zipCode: null }
export default {
  name: 'SysOrg',
  components: { pagination, crudOperation, rrOperation, udOperation },
  mixins: [presenter(), header(), form(defaultForm), crud()],
  cruds() {
    return CRUD({ title: '机构表', url: 'api/sysOrg', idField: 'orgId', sort: 'orgGrade,desc', crudMethod: { ...crudSysOrg }})
  },
  data() {
    return {
      permission: {
        add: ['admin', 'sysOrg:add'],
        edit: ['admin', 'sysOrg:edit'],
        del: ['admin', 'sysOrg:del']
      },
      rules: {
        orgId: [
          { required: true, message: '机构id不能为空', trigger: 'blur' }
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
