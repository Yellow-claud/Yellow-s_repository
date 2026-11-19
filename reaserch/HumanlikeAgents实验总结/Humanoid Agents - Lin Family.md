# Humanoid Agents · Lin Family

## 实验内容

Eddy Lin 和 John Lin 在 Lin Family 场景中度过一个模拟日。日志覆盖 2023-01-03 06:00–23:45，每 15 分钟记录两名角色的状态和行动。本次使用 `deepseek-flash`。

## 日志可观察的机制

- **需求与人物状态**。每帧记录饱腹、社交、娱乐、健康、精力，还包含当前位置、情绪及人际关系亲密度。原日志字段包括 `basic_needs`、`location`、`emotion` 和 `social_relationships`。
- **日程与短时计划**。同一角色状态里同时有日计划 `most_recent_day_plan`、15 分钟计划 `most_recent_15m_plan` 和当时的活动 `activity`。可以按时间并排查看计划与实际动作。
- **调整建议**。`most_recent_suggested_change` 单独记录建议。可以把建议与后续动作对照，日志中的先后关系本身无法证明建议导致了该动作。

## 对应数据

72 个时间点，共 144 条人物状态记录。下表是各角色在本次运行中观测到的最小值和最大值。

| 人物 | 饱腹 | 社交 | 娱乐 | 健康 | 精力 | 建议字段非空的帧 |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Eddy Lin | 5–10 | 5–10 | 0–10 | 0–8 | 3–10 | 48 / 72 |
| John Lin | 5–10 | 4–10 | 2–10 | 5–10 | 0–10 | 25 / 72 |

**记录示例。** 23:15，Eddy 的精力是 3，日志建议现在刷牙、随后换睡衣以便早点睡。这一帧的动作是 `brush teeth`，23:30 的动作是 `change into pajamas`。这是同一个角色的需求、建议与后续动作可以对齐的样本。

### 需求和执行动作对照

抽取日内 8 个时间点，每个时间点保留两人的状态。需求值依次为饱腹、社交、娱乐、健康、精力。

| 模拟时间 | 人物 | 需求值 | 情绪 | 实际动作（日志原文） |
| --- | --- | --- | --- | --- |
| 06:00 | Eddy Lin | 5 / 5 / 4 / 5 / 10 | neutral | sleep |
| 06:00 | John Lin | 5 / 5 / 4 / 5 / 10 | neutral | wake up and turn off the alarm |
| 10:00 | Eddy Lin | 9 / 6 / 1 / 0 / 8 | neutral | travel to oak hill college |
| 10:00 | John Lin | 9 / 10 / 9 / 10 / 7 | neutral | review incoming prescriptions for accuracy and completeness |
| 12:00 | Eddy Lin | 10 / 10 / 1 / 1 / 8 | neutral | cancel campus cafe lunch with monica moreno |
| 12:00 | John Lin | 10 / 10 / 6 / 10 / 6 | neutral | gather lunch items |
| 14:00 | Eddy Lin | 9 / 9 / 4 / 0 / 10 | neutral | cancel or postpone scheduled music work |
| 14:00 | John Lin | 10 / 10 / 7 / 10 / 5 | neutral | follow up with customers on pending issues |
| 16:00 | Eddy Lin | 9 / 10 / 7 / 1 / 10 | neutral | rest instead of guided ear-training exercises |
| 16:00 | John Lin | 8 / 10 / 10 / 9 / 2 | neutral | skip the political chat with tom moreno |
| 18:00 | Eddy Lin | 9 / 9 / 8 / 4 / 8 | neutral | warm up with scales and arpeggios |
| 18:00 | John Lin | 8 / 10 / 9 / 10 / 0 | neutral | collect prescription details and check insurance |
| 20:00 | Eddy Lin | 9 / 10 / 10 / 6 / 6 | happy | gather with family in the dining area |
| 20:00 | John Lin | 9 / 10 / 5 / 9 / 2 | happy | gather with family for an earlier, simpler dinner |
| 22:00 | Eddy Lin | 10 / 10 / 10 / 5 / 4 | surprised | watch the climax of the movie |
| 22:00 | John Lin | 10 / 10 / 10 / 10 / 5 | neutral | pause briefly for snacks and a bathroom break |

18:00，John 的精力记录为 0，同一帧还记录了收集处方资料、核对保险的动作。14:00，Eddy 的健康记录为 0，同一帧的动作是取消或推迟音乐工作。

### 分时段建议记录

统计建议字段非空的帧数。每个时段每人有 12 个采样点。

| 模拟时段 | Eddy Lin | John Lin |
| --- | --- | --- |
| 06:00–08:45 | 7 | 2 |
| 09:00–11:45 | 12 | 0 |
| 12:00–14:45 | 12 | 0 |
| 15:00–17:45 | 8 | 9 |
| 18:00–20:45 | 2 | 11 |
| 21:00–23:45 | 7 | 3 |

### 情绪、地点与关系

情绪和地点按人物状态帧计数。地点取日志位置字段的第一层，亲密度取双方各自对对方的记录。

| 人物 | 情绪（帧数） | 地点（帧数） | 06:00 → 23:45 亲密度 |
| --- | --- | --- | --- |
| Eddy Lin | neutral 58、happy 9、sad 4、surprised 1 | Lin family's house 62、Oak Hill College 9、Hobbs Cafe 1 | 5 → 15 |
| John Lin | neutral 61、happy 9、sad 2 | The Willows Market and Pharmacy 47、Lin family's house 25 | 5 → 15 |

[原始日志](run.log) · [逐帧需求](需求.md) · [逐帧建议](建议.md) · [逐帧行为](行为.md)
