- ## 基于 G6 需求可行性  
	- 整体节点布局  
		- 基于 [同心圆 Concentric Layout](https://g6.antv.vision/zh/docs/api/graphLayout/concentric) 进行调整，实现不同层级节点直线连接，同时调整节点间连接半径，控制连接距离  
	- 节点渲染  
		- 多个节点 文本超长情况下，并且需要进行悬浮提示，内置节点不支持配置 title 展示完整字段，需要进行自定义节点配置。自定义节点为 内置图形 Shape 的组合，其实也就是内置的节点类型进行再组装。Shape 类型除了 DOM 可以通过配置 html 外，其他 Shape 还是不能满足悬浮提示完整字段功能。  
			- DOM 类型只支持原生 HTML DOM ，不支持各类 react vue 组件。  
			- 通过DOM配置之后，需要额外处理DOM的交互事件  
			- DOM 配置之后，由于有图标，有文字，整体大致为长方形，由于需要才图标中心穿过，默认连接点为 DOM 左上角，因此需要 getAnchorPoints 重新计算锚点 ---- **存在风险**  
		- 使用内置 tooltip 则存在悬浮图标、文本都会触发浮层提示  
	- 节点、边 hover 、click 事件，状态处理  
		- 节点、边使用内置组件，可以通过配置状态处理，若涉及到 DOM 类型，则需要额外特殊处理  
	- 浮层展示  
		- tooltip 不支持传入组件， 通过点击节点触发事件，再调整画布外的组件的定位，需要处理自定义浮层边缘时场景  
	- 未实现/实现困难  
		- 外层节目右上角数字标识、省略号标识，若需要 title 提示，目前除再构造新节点外无其他想法  
		- 强化、弱化效果：外层节点的弱化效果目前由于是自定义节点实现起来有困难  
		- 外层连接中间层 锚点坐标计算未实现  

弱化效果已实现
数字标识已实现
锚点使用当前布局实现有问题，绘制时获取不到当前节点坐标、角度。linkPoints 只是配置默认锚点是否展示，不能修改其位置。