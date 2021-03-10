# el-Tooltip-
基于el-Tooltip 文字提示二次封装
全局注册后使用
<div class="text-ide">
	<ellipsis-tooltip :text="scoped.row.planName" placement="top">
	</ellipsis-tooltip>
</div>
//注意样式
	.text-ide {
		overflow: hidden;
		display: -webkit-box;
		text-overflow: ellipsis;
		-webkit-line-clamp: 1;
		-webkit-box-orient: vertical;
		white-space: normal;
	}

