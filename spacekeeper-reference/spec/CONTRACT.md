# SpaceKeeper 数据协议 v0.1

## 设计边界
统一 **交换数据**，不统一 **Agent 的性格、绘图方式、算法语言或生图模型**。主场景文档是任何 Agent 的最低共同语言。没有场景一致性需求时，不必创建。数据允许不完整，但不允许将猜测伪装成确定事实。

## 文件格式
UTF-8 JSON；文件名建议 `<scene_id>.scene.json`。须满足 `scene.schema.json`。根字段：

| 字段 | 含义 |
|---|---|
| `format` | 固定 `spacekeeper.scene`，供接手 Agent 识别 |
| `version` | 固定 `0.1`；不兼容版本须转换后再处理 |
| `scene_id` | 全局稳定场景 ID |
| `revision` | 场景事实或镜头定义每次编辑递增，避免旧结果误复用 |
| `title` | 场景可读名称 |
| `axes` | 固定 `x_east_y_north`，北上东右，**不能随镜头旋转** |
| `entities` | 人物、动物、道具、地标、墙门、区域；用稳定 ID |
| `shots` | 镜头清单（顺序即时间顺序），包括相机定义、参考图和可选检查结果 |
| `events` | 在某镜头前生效的实体位置变化；无变化留空数组 |

### `entities[]` 核心字段
- `id`：稳定英文 snake_case 标识，如 `chair_w`, `dog_1`。不可使用“左边那个椅子”等随镜头变化的名字做 ID。
- `label`：供提示词用的可读名称，如 `西侧椅子`。
- `kind`：`character | animal | prop | structure | landmark | zone`。
- `fixed`：是否默认固定；人物、动物通常 `false`，门、树、池塘通常 `true`。
- `location` 三选一：
  1. `{"xy":[-1,0],"certainty":"given"}`：粗略坐标，单位任意，精度不要求高。`given` 是剧本/用户明确给定；`inferred` 为 Agent 推定，遇到矛盾必须让位。
  2. `{"relative_to":"chair_w","relation":"at","certainty":"given"}`：通过另一个实体锚定。适合“甲坐西侧椅子”“小狗靠东墙”；`near` 不等于精确位置。
  3. `{"unknown":true}`：不知道，不能强行投影。
- `relations` 可选：补充相邻、靠近、朝向等信息，例如 `{"kind":"near","target":"wall_e"}`。不要重复矛盾关系。

### `shots[]` 核心字段
- `id`：稳定镜头 ID，依数组顺序构成故事顺序。
- `camera.position` 和 `camera.target`：粗略二维坐标，`position` 不得等于 `target`。
- `framing`：`wide | medium | close | detail`，用于判断谁可能被裁切。不是物理焦距。
- `focus_ids`：镜头关注对象；未列出的实体可以不出现在图里。
- `must_show_ids`：**必须出现**的对象；没有在图片里看到这些对象时才值得检查缺失。
- `reference_image`：可选文件路径或图像 URI；不作为场景事实。
- `space_prompt`：可选，当前空间逻辑的简短提示词缓存；任何相关空间/机位编辑后必须重算。
- `review`：可选检查结果，`pass | uncertain | fail | unchecked`；`issues` 描述冲突，不应直接改权威位置。

### `events[]` 核心字段
- `before_shot_id`：从哪个镜头开始采用新位置。
- `entity_id`：改变位置的实体。
- `new_location`：与实体 `location` 同一格式。
- `reason`：剧情原因。事件按镜头顺序累计应用，旧镜头不受影响。

## 确定性与推断的边界
1. 先根据 `location`、已有 `events` 得到镜头时刻的位置。`at` 等确定锚点可继承坐标；`near` 只传递邻近关系，不能随意转换成精确坐标。
2. 若坐标已知，摄影机方向 `F = normalize(target - position)`，画面右方向 `R = (F_y, -F_x)`。左右由 `dot(P-C,R)` 判断；远近由 `dot(P-C,F)` 比较，接近零视为中间。阈值应根据该场景对象的跨度粗分，不能固定为厘米。
3. `left/center/right` 是 **相对当前镜头的画面方位**；`north/south/east/west` 是 **永久场景方位**。两者不能混用。
4. 画面上/下、可见/不可见、遮挡和镜头外不能只由一张俯视图精确保证：应结合景别、对象体积、实际图像和导演意图判断；不确定时标 `uncertain`。
5. 构图好看可以优先于厘米级准确，但不得无因换人、换座位、颠倒关键地标或反转剧情动作。
6. 图像模型是创作输出，不是空间事实源。检图失败优先修镜头的生图提示词。更新场景事实必须有用户、剧本或明确剧情事件依据。

## 结构之外必须做的语义校验
JSON Schema 只检查数据形状；实际 Agent 还必须检查：`entities[].id` / `shots[].id` 在各自列表中唯一，所有 `relative_to`、`relations[].target`、`focus_ids`、`must_show_ids`、`events[].entity_id`、`events[].before_shot_id` 引用均存在；相机位置不等于目标；位置的相对引用不能形成循环；剧情动作不得让两个互斥座位同时被同一角色占据。若校验不通过，不得静默生成自相矛盾的镜头提示词。

## 交接最低检查
新 Agent 读文件后，应能回答：这是哪个场景、东西南北在哪里、有哪些稳定 ID、谁靠近谁、当前镜头从哪里拍、有没有发生过移动、哪些结论只是推断、最近参考图和校验结果在哪里。若不能，说明数据缺失或含糊，标为未知并向上层工作流报告，不得暗中补全。

## 扩展兼容
所有对象允许 `extensions` 字段，供自选绘图技术和项目集成保存额外信息。基础工具必须忽略不认识的扩展；不得重定义 `id`、`axes`、`location` 或相机含义。版本升级不得静默更改既有字段语义。
