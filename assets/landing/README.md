# Landing 素材说明

> 产品素材总规则见 [`docs/产品/产品素材系统.md`](../../../../docs/产品/产品素材系统.md)。本目录只说明 Landing 品牌叙事产物，不承担产品素材 SSOT。

## 重要边界

`product-story*.mp4` 与 `journey-listen.jpg` 来自 `brand-film/` 下的 React / CSS 舞台复刻，属于**品牌叙事素材**。

它们可以用于讲述知与行的产品旅程和品牌气质，但**不是当前 App 的真机录屏或产品真实性证明**。页面、文案与渠道发布不得把这些文件描述为“真实 App 画面”“真机录屏”。

Landing 若要证明“产品现在真的长这样、真的能完成这些动作”，必须另用当前候选正式构建产生的真实 Simulator / 真机截图与录屏，具体规则见产品素材 SSOT。

## 当前品牌片

当前品牌片主线为：

> **认清当下的矛盾 → 为自己走一步 → 看看变化慢慢发生。**

产品主片使用固定文件名：

- `product-story.mp4`：横版 1920×1080；
- `product-story-poster.jpg`；
- `product-story-portrait.mp4`：竖版 1080×1920；
- `product-story-portrait-poster.jpg`。

横版由 `npm run render:brand-film` 导出；竖版由 `npm run render:brand-film-portrait` 导出。舞台分别位于 `brand-film/stage/` 与 `brand-film/portrait-stage/`。

`journey-listen.jpg` 是竖版舞台的叙事静帧，由 `npm run render:brand-film-portrait:stills` 导出；重渲竖版成片时一并更新。

## 状态纪律

- 品牌片母线、关键产品语义变化时，重新渲染；
- 轻微 UI 间距 / 阴影变化不要求单独重渲品牌片；
- 品牌片可以继续使用源码复刻，但不得进入 App Store 产品证据集；
- App Store、App Preview 与 Landing 的“真实产品旅程”必须从同一个锁定构建重新录制；
- 旧 topic films 与旧产品截图是否可继续分发，由 `docs/产品/产品素材系统.md` 的当前资产裁决决定。
