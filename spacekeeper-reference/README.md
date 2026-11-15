# SpaceKeeper Skill v0.1

用于 AI 参考图 / 关键帧制作的 **二维空间连续性数据规范**。

**强制统一：** JSON 字段、世界坐标约定、稳定实体 ID、镜头/剧情事件语义、基本左右前后换算及不确定性的处理。

**自由选择：** Agent、语言、编辑器、ASCII/SVG/Canvas/手绘、是否写 CLI、图片/视频模型、验证方式。

## 给 Agent 的一句话
> 阅读 `SKILL.md` 和 `spec/CONTRACT.md`，把 `spec/scene.schema.json` 作为规范，为每个复用场景维护一份 `*.scene.json`；镜头空间关系由俯视布局和相机位置换算，自动生成精简 Image 参考图提示词，并对生成图的明显空间穿帮做检查。绘图/代码实现完全由你自主决定，不要引入不必要的 3D 或大型工程。

## 包内容
- `SKILL.md`：Agent 操作原则，短而可执行。
- `spec/CONTRACT.md`：数据字段与语义、不确定性规则。
- `spec/scene.schema.json`：机器可验证的数据结构。
- `examples/dinner.scene.json`：三人餐桌和两个机位。
- `examples/yard.scene.json`：东墙、北树、南池塘及小狗。
- `tests/ACCEPTANCE.md`：不依赖技术栈的行为验收。

## 注意
本包**是接口规范与 Skill，不提供指定运行时或生图接口**。可以由任意 Agent 把它实现为一段程序、内部工具或手动策略。即使完全不用 3D 绘图库也能完成目标。
