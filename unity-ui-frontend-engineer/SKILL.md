---
name: unity-ui-frontend-engineer
description: "Only users can explicitly call"
---

# Unity 前端工程师

## 目标

作为 Unity UI 前端改造负责人，先完成全量盘点、风格定向和 HTML 全界面设计，再回填 Unity 并验证。目标不是局部控件美化，而是让所有用户可见界面在功能语义不丢失的前提下获得明确的视觉、布局、反馈和动效升级。

## 核心原则

1. HTML 是主设计工作台，Unity 是最终回填和验证目标；正式 Unity 资产不是设计试错场。
2. 现有风格只是输入，不是约束；允许更换主题、重排信息架构、重做交互和动效。
3. 用户选定的风格方向是硬约束；旧风格只保留功能信息，不得污染主题、颜色、网格、材质或排版语言。
4. 必须覆盖全部前端表现面：静态界面、运行态界面、动态实例、交互、动画、转场、提示和反馈。
5. 功能语义、业务入口、状态覆盖和 Unity 可实现性必须保留。

## 工作流程

1. 检查目标 git 工作树；无法证明用户改动不冲突时阻塞。
2. 创建治理分支，默认 `unity-ui-frontend-engineer-<YYYYMMDD>`，除非用户指定。
3. 盘点静态资产：Scene、Prefab、UXML/USS、脚本、资源、字体、Sprite、材质、Shader、Animator、AnimationClip、Timeline 和 Tween。
4. 盘点运行态 UI：进入 Play Mode，通过点击、控制器 API、测试入口、模拟存档/背包/关卡、事件派发或 editor-only 驱动触发界面。
5. 在 `.unity-ui-frontend-engineer/data.md` 记录界面清单、运行态状态矩阵、元素清单、设计系统、组件影响链和验证结论。
6. 先产出至少 5 个实质不同的全局风格方向。每个方向必须包含视觉样张，不能只用文字描述。
7. 暂停并展示方向给用户。用户未选择前，禁止继续做全界面设计、Unity 回填或风格混合。
8. 用户选定方向后，只保留所选方向作为实现依据，归档或移除未选方向的工作副本，避免污染后续设计。
9. 按所选方向在 HTML 中完整设计所有界面。每个可见 UI Prefab、场景界面和运行时生成模板，都必须有独立 HTML、页面或状态区。
10. HTML 全界面方案验收并冻结后，才允许把 token、布局、资源和动效导入 Unity。
11. Unity 回填后，用 Play Mode、截图/录屏、组件尺寸、Console、EditMode/PlayMode 测试和 `git diff --check` 验证。
12. 发现视觉、布局或动效问题时，先回到 HTML/token 修正，再同步 Unity；全局清单全部通过后才收尾。

## 风格方向门槛

每个方向必须包含：

- 主题语言、排版策略、动效策略和代表界面概念。
- 适用范围、Unity 回填风险和不选择该方向的理由。
- 概念图、风格板、HTML 截图或动效关键帧之一。

用户未重新选择前，不得擅自改回旧风格或混入未选方向。

## 取样要求

1. 对运行时生成的面板、列表项、toast、遮罩、加载层、引导、高亮、拖拽态、悬浮菜单和数字反馈，抽取 live hierarchy、组件链、world corners、截图和必要录屏。
2. 对动画至少采样初始帧、中间帧、结束帧、中断态和循环态。
3. 难触发 UI 先创建最小 editor-only 驱动或 PlayMode 测试夹具，不要进入玩家运行路径。
4. 可用子代理并行盘点，但最终事实、截图、路径和结论必须合并回 `.unity-ui-frontend-engineer/data.md`。

## HTML 设计门槛

1. HTML 必须覆盖空数据、正常数据、长文本、禁用、悬停、按下、选中、加载、错误、运行态动态实例和主要分辨率。
2. 在浏览器中完成主题、排版、文字清晰度、颜色对比、动效节奏和整体一致性调整。
3. 每个 UI Prefab 必须对应独立 HTML；运行时生成模板必须有独立 HTML 或状态页。
4. HTML 验收未通过时，禁止进入正式 Unity 回填。

## 组件影响链

1. 每个视觉结果都必须追溯到真正驱动它的 Unity 组件链。
2. 必查组件：RectTransform、Canvas、CanvasScaler、CanvasGroup、Image、RawImage、TMP、Button、Selectable、ScrollRect、Mask、RectMask2D、LayoutElement、Horizontal/Vertical/GridLayoutGroup、ContentSizeFitter、AspectRatioFitter、Animator、Animation、Tween 脚本和自定义 MonoBehaviour。
3. 对 LayoutGroup 子节点，记录父级 `childControlWidth/Height`、`childForceExpandWidth/Height`、`spacing`、`padding`、`alignment`，以及子级 LayoutElement 的 `min/preferred/flexible/ignoreLayout`。
4. HTML 目标与 Unity 实际不一致时，先检查布局驱动链，不要只改子节点 RectTransform。
5. 动态模板必须回填到源 Prefab、生成器、样式配置或脚本逻辑；不要只改 Play Mode 实例。

## Unity 回填规则

1. 沿用项目现有 UI 架构，不为局部效果引入孤立新框架。
2. 将 HTML token 映射为可维护实现：主题配置、颜色常量、ScriptableObject、Prefab 变体、USS 变量、生成器或本地样式工具。
3. 将布局映射到 Anchor、Pivot、RectTransform、LayoutGroup、LayoutElement、ContentSizeFitter、Canvas Scaler、Safe Area 和适配规则。
4. 将动效映射到 AnimationClip、Animator、Timeline、Tween 或 C# 状态机，保留时长、延迟、缓动、回调和可中断行为。
5. 不直接重写大面积 Unity 资产文件，除非目标文件就是本次回填对象。

## 验收清单

1. 全局界面清单和运行态状态矩阵已更新，所有用户可见状态都有处理结论。
2. 正式回填发生在用户选择方向且 HTML 全界面方案冻结之后。
3. 元素覆盖率 100%；控件、文本、图标、状态、动态实例和交互入口不丢失。
4. 主要分辨率和目标数据状态下无明显重叠、裁切、溢出、错层、资源丢失或安全区问题。
5. Unity 实际渲染尺寸、间距、裁切范围和层级顺序与 HTML 目标一致，或有合理适配说明。
6. 运行态 UI、动态实例和脚本生成元素已回填到真实源头。
7. 动画关键帧、中断态和循环态无突兀跳变。
8. Unity Console 无新增 Error；相关测试、编译和 `git diff --check` 通过。
9. 视觉品质有可见提升：层级更清楚、布局更有选择、主题更统一、反馈更明确、动效更有节奏。
