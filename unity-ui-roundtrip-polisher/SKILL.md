---
name: unity-ui-roundtrip-polisher
description: "Only users can explicitly call"
---

# Unity 前端工程师


## 主流程

1. 检查工作区是否干净，不干净则提醒用户清理，并直接结束。
2. 检查是否有 Unity 相关的 mcp 工具。
3. 了解项目文档什么的。
4. 

2. 盘点所有用户可见前端：静态界面、运行态界面、动态实例、交互、动画、转场、提示和反馈。
3. 在 `work/unity-ui-html-loop/` 记录界面清单、运行态状态矩阵、元素清单、设计系统和组件影响链。
4. 先产出至少 5 个实质不同的全局风格方向概念图；只写 `work/`，禁止改正式 `Assets/`。
5. 暂停，等待用户选择方向；用户未选择前禁止继续。
6. 用户选择后，按所选风格在 HTML 中完整设计所有界面；每个 UI Prefab 必须对应一个独立 HTML，运行时生成模板必须有独立 HTML 或状态页。
7. 在浏览器里统一调整主题、排版、文字对比、状态、动效和响应尺寸，直到全界面 HTML 通过验收。
8. HTML 全界面方案冻结后，才允许把 token、布局、资源和动效导入 Unity。
9. Unity 导入后用 Play Mode、截图/录屏、组件尺寸、Console 和测试验证；发现视觉或布局问题，先回 HTML/token 修正，再同步 Unity。
10. 全局清单中的界面、运行态状态、动态模板和动画转场全部通过后，才允许收尾。

## 风格选择门

1. 风格选择门是强制步骤，不能自行跳过。
2. 至少 5 个方向，每个方向必须包含主题语言、排版策略、动效策略、代表界面概念图、适用范围、Unity 回填风险和不选择它的理由。
3. 每个方向必须有概念图、风格板、HTML 截图或动效关键帧之一；不能只用文字描述。
4. 用户选定方向后，所选风格是硬约束；现有旧风格只保留功能信息，不得反向污染主题、颜色、网格、材质或排版语言。
5. 用户未重新选择前，不得擅自改回旧风格或混入未选方向。

## HTML 全界面设计门

1. Unity 正式资产不是设计试错场；Prefab 回填前必须先在 HTML 中调好。
2. 每个可见 UI Prefab、场景界面和动态模板都必须有对应 HTML 文件、页面或状态区。
3. HTML 必须覆盖空数据、正常数据、长文本、禁用、悬停、按下、选中、加载、错误、运行态动态实例和主要分辨率。
4. 在浏览器中完成主题、排版、文字清晰度、颜色对比、动效节奏和整体一致性调整。
5. HTML 验收未通过时，禁止进入正式 Unity 回填。

## 设计原则

1. 负责全部前端表现面，不做局部控件美化。
2. 现有风格只是输入，不是牢笼；允许更换主题、重排信息架构、重做交互和动效。
3. 必须明显升级；不得只改字号、边距、颜色和边框。
4. 功能语义、业务入口、状态覆盖和 Unity 可实现性必须保留。
5. HTML 是主设计工作台，Unity 是最终回填和验证目标。

## 取样要求

1. 静态取样：Scene、Prefab、UXML/USS、脚本、资源、字体、Sprite、材质、Shader、Animator、AnimationClip、Timeline、Tween。
2. 运行态取样：必须进 Play Mode，通过点击、控制器 API、测试入口、模拟存档/背包/关卡、事件派发或 editor-only 驱动触发 UI。
3. 对运行时生成的面板、列表项、toast、遮罩、加载层、引导、高亮、拖拽态、悬浮菜单和数字反馈，抽取 live hierarchy、组件链、world corners、截图和必要录屏。
4. 对动画至少采样初始帧、中间帧、结束帧、中断态和循环态。
5. 难触发 UI 先创建最小 editor-only 驱动或 PlayMode 测试夹具；不得进入玩家运行路径。

## 组件影响链

1. 每个视觉结果都必须追溯到真正驱动它的 Unity 组件链。
2. 必查组件：RectTransform、Canvas、CanvasScaler、CanvasGroup、Image、RawImage、TMP、Button、Selectable、ScrollRect、Mask、RectMask2D、LayoutElement、Horizontal/Vertical/GridLayoutGroup、ContentSizeFitter、AspectRatioFitter、Animator、Animation、Tween 脚本和自定义 MonoBehaviour。
3. 对 LayoutGroup 子节点，必须记录父级 `childControlWidth/Height`、`childForceExpandWidth/Height`、spacing、padding、alignment，以及子级 LayoutElement 的 min/preferred/flexible/ignoreLayout。
4. HTML 目标与 Unity 实际不一致时，先检查布局驱动链；不得只改子节点 RectTransform。
5. 动态模板必须回填到源 Prefab、生成器、样式配置或脚本逻辑；不要只改 Play Mode 实例。

## 回填规则

1. 沿用项目现有 UI 架构，不为局部效果引入孤立新框架。
2. 将 HTML token 映射到 Unity 可维护实现：主题配置、颜色常量、ScriptableObject、Prefab 变体、USS 变量、生成器或本地样式工具。
3. 将布局映射到锚点、Pivot、RectTransform、LayoutGroup、LayoutElement、ContentSizeFitter、Canvas Scaler、Safe Area 和适配规则。
4. 将动效映射到 AnimationClip、Animator、Timeline、Tween 或 C# 状态机，保留时长、延迟、缓动、回调和可中断行为。
5. 不直接重写大面积 Unity 资产文件，除非目标文件就是本次回填对象。

## 验收门槛

1. 全局界面清单和运行态状态矩阵均已更新，所有用户可见状态都有处理结论。
2. 正式回填发生在用户选择方向且 HTML 全界面方案冻结之后。
3. 元素覆盖率 100%；控件、文本、图标、状态、动态实例和交互入口不丢失。
4. 主要分辨率和目标数据状态下无明显重叠、裁切、溢出、错层、资源丢失或安全区问题。
5. 关键布局元素的 Unity 实际渲染尺寸、间距、裁切范围和层级顺序与 HTML 目标一致，或有合理适配说明。
6. 运行态 UI、动态实例和脚本生成元素已回填到真实源头。
7. 动画关键帧、中断态和循环态无突兀跳变。
8. Unity Console 无新增 Error；相关 EditMode/PlayMode 测试、编译和 `git diff --check` 通过。
9. 视觉品质有可见提升：层级更清楚、布局更有选择、主题更统一、反馈更明确、动效更有节奏。
