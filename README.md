# Whisper-of-Nothingness-Game

本游戏由本人独立使用Unity开发。

使用插件：DoTween，UniTask。

## 操作说明

- Space：开始游戏。
- WASD：运动。
- Z：在紫色方块上按z休息（如果是第一次接触该紫色方块，则第一次按z只是点燃而非休息）并存档。实际上，和黑暗之魂的篝火的逻辑完全相同。
- BackSpace：退出游戏（不保存）。

## 地图编辑

**游戏存档与地图信息路径**：`Whisper of Nothingness\Whisper of Nothingness_Data\Data`（如果你发现里面有一些".meta"文件，你可以删除它们，它们完全没用）

- 在mapData文件夹中，文件夹名称为*地图关卡名*（暂未开发切换关卡功能，请把需要加载的地图的文件夹名称设为“0”）；
- 文件夹里面的txt文件的文件名则为对应关卡的*地图层数*，如最低层的地图数据就会存在“0.txt”当中。

实际上，最佳的编辑地图的方式是使用*Excel*编辑（把单元格的宽高设为一致，开设多个sheet，每个sheet代表一层），然后把每个sheet保存为txt文件。

### 地图格式要求

其实没什么要求——前提是在Excel转txt的时候别出现奇怪的位置偏移。我在第一行和第一列放置“#”来防止这种事情发生。

### 方块功能与对应符号表示

看代码捏

```cs
public BlockTypeEnum transStrToType(string blockTypeStr) {
    switch (blockTypeStr) {
        case "0"://完全没有额外功能的棕色方块
            return BlockTypeEnum.defaultType;
        case "reborn"://紫色的休息（重生）方块
            return BlockTypeEnum.rebornType;
        case "-"://每个地图的最初出生点，请保证每张地图只有一个，否则将随机指定
            return BlockTypeEnum.rebornType;
        case "jump"://触碰时跳跃。跳跃有CD。
            return BlockTypeEnum.jumpType;
        case "cure"://触碰后清空buff，生成绿色粒子，给予回血。只能用一次，休息后恢复使用
            return BlockTypeEnum.cureType;
        case "fire"://触碰后获得火焰buff，加速，受到灼烧伤害
            return BlockTypeEnum.fireType;
        case "ice"://触碰后获得冰buff，减速
            return BlockTypeEnum.iceType;
        case "owdE"://接下来是四种单向门，只有在球碰到特定方向的那一面后，方块的碰撞箱就会消失，可以通过。休息、读档后依旧不变
            return BlockTypeEnum.onewayDoor_E;
        case "owdS":
            return BlockTypeEnum.onewayDoor_S;
        case "owdW":
            return BlockTypeEnum.onewayDoor_W;
        case "owdN":
            return BlockTypeEnum.onewayDoor_N;
        case "wood"://当球上有火焰buff的时候，碰撞则该方块消失。休息后重现
            return BlockTypeEnum.woodBoxType;
        default://如果发现有方块没出现，就看看是不是打错字了
            return BlockTypeEnum.empty;
    }
}
```
    
## 展望

### 可迭代功能
- 目前，项目提供了非常大的迭代空间，耦合度也适当。
- 明显可接着开发的功能：关卡切换、buff添加、钥匙系统、物品拾取系统、更多的特殊方块……
- buff可以规定相容、互斥关系以及优先级排序。
- 另外，打算添加MessageBox，碰撞后显示对应信息，信息也保存在外部txt文件中。

### 初衷与感想

玩魂、狼、空洞骑士、东方等等游戏的时候，很多游戏设计灵感涌现出来，但苦于网上找不到可快速做游戏的东西。于是，一半是想做自己的游戏、一半是给大家提供快速构建灵感的道路地做出来了这个东西。实际上，有的功能还不够完善严谨，本人也是第一次写大项目，而且是自己独立开发，经历了挺多困难，也学到了不少。接下来继续努力吧。
