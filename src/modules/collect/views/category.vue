<template>
	<cl-crud ref="Crud">
		<el-row>
			<!-- 刷新按钮 -->
			<cl-refresh-btn />
			<!-- 新增按钮 -->
			<cl-add-btn />
			<!-- 删除按钮 -->
			<cl-multi-delete-btn />
			<cl-flex1 />
			<!-- 关键字搜索 -->
			<cl-search-key />
		</el-row>

		<el-row>
			<!-- 数据表格 -->
			<cl-table ref="Table" />
		</el-row>

		<el-row>
			<cl-flex1 />
			<!-- 分页控件 -->
			<cl-pagination />
		</el-row>

		<!-- 新增、编辑 -->
		<cl-upsert ref="Upsert" />
	</cl-crud>
</template>

<script lang="ts" name="collect-category" setup>
import { useCrud, useTable, useUpsert } from "@cool-vue/crud";
import { useCool } from "/@/cool";

const { service } = useCool();

// cl-upsert 配置
const Upsert = useUpsert({
	items: [
		{ label: "名称", prop: "cat_name", required: true, component: { name: "el-input" } },
		{
			label: "描述",
			prop: "cat_desc",
			component: { name: "el-input" },
			required: false
		},
		{ label: "图标", prop: "cat_icon", component: { name: "cl-upload" }, required: false },
		{ label: "等级", prop: "cat_level", required: true, component: { name: "el-input" } }
	]
});

// cl-table 配置
const Table = useTable({
	columns: [
		{ type: "selection" },
		{ label: "ID", prop: "id" },
		{ label: "名称", prop: "cat_name" },
		{ label: "描述", prop: "cat_desc" },
		{ label: "图标", prop: "cat_icon", component: { name: "cl-image", props: { size: 60 } } },
		{ label: "等级", prop: "cat_level" },
		{ label: "创建时间", prop: "createTime" },
		{ label: "更新时间", prop: "updateTime" },
		{ type: "op", buttons: ["edit", "delete"] }
	]
});

// cl-crud 配置
const Crud = useCrud(
	{
		service: service.collect.category
	},
	(app) => {
		app.refresh();
	}
);
</script>
