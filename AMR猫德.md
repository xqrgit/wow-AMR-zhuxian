AMR战斗历程
==
猫德
==
>http://www.askmrrobot.com/wow/theory/rotation/amrdruidferaldefault?spec=DruidFeral&version=live

>源文件

***
###名词解释
`FeralBleedSnapshot 是个变量 需要一个函数进行计算，附在后面`
`RipBuffs 是一个变量，附在后面`
`RakeBuffs 是一个变量，附在后面`
***

1.  变猫
2.  释放 嗜血
3.  if 有潜行buff 

	释放 斜掠
4. if 猛虎之怒冷却时间小于12秒 

	释放 化身：艾露恩之卷
5. if （没有节能施法buff AND 能量缺少值大于等于60） OR 能量缺少值大于等于80

	释放 猛虎之怒
6. if 有猛虎之怒的buff

	释放 狂暴
7. if 有猛虎之怒buff OR 化身：艾露恩的buff可持续时间大于20秒 OR 目标预计死亡时间小于30秒

	进入 **Cooldown** Action
8. if 目前连击点数=0 AND 当前能量 大于 释放凶猛撕咬所需最大能量值

	释放 化身：艾露恩之眷
9. if 有割裂DOT AND 可以刷新割裂DOT AND 目标预计死亡时间大于3秒 AND （目标血量低于百分之25 OR 有天赋剑齿利刃

	释放 凶猛撕咬
10. if 有天赋血腥爪击 AND 有掠食者的迅速BUFF AND 没有血腥爪击的buff AND [连击点数大于等于5 OR 掠食者的迅速buff还可持续时间小于等于GCD OR （连击点数等于2 AND 安莎曼的狂乱CD时间小于等于GCD）]

	释放 愈合
11. if 连击点数大于等于5 then 

	return **Finshiners** ACTION
12. if 连击点数大于等于3 AND 没有月神的守护buff AND [（有血腥爪击buff OR 没有血腥爪击天赋） AND （有野蛮咆哮buff OR 没有野蛮咆哮天赋）]

	释放安莎曼的狂乱
13. if 连击点数小于等于4 then

	return **Generators** ACTION
***
===

*定义*  **Finisher** ACTION

1. if [连击点数乘以（1+神器锋锐利齿特质的层数乘以0.07）乘以*FeralBleedSnapshot* 大于 RipBuffs的伤害峰值] AND (有野蛮咆哮buff OR 没有野蛮咆哮天赋)

	释放 割裂
2. if 能量大于等于释放凶猛撕咬的最大所需能量 AND 有割裂DOT AND 有天赋剑齿利刃天赋

	释放 凶猛撕咬
3. if 割裂dot可以刷新 AND （有凶猛咆哮buff OR 没有凶猛咆哮天赋）AND 没有剑齿利刃天赋

	释放 割裂（此时为多目标模式，最多5个）

>DOT可以刷新的意思请参见暗牧翻译
>
>多目标模式 意思请参见暗牧翻译

4. if 野蛮咆哮的buff持续时间小于12秒

	释放 野蛮咆哮
5. if 能量大于等于释放凶猛撕咬的最大所需能量 AND [割裂DOT可持续时间大于等于(割裂总持续时间/2） AND 野蛮咆哮buff持续时间大于等于12秒 OR 没有野蛮咆哮天赋]

	释放 凶猛撕咬

***
===

*定义*  **Generators** ACTION

1. if 有猛虎之怒buff AND （有野蛮咆哮buff OR 没有野蛮咆哮天赋） AND （有血腥爪击buff OR 没有血腥爪击天赋） AND 能够释放斜掠

   释放 影遁
2. if 【没有斜掠DOT or （没有天赋血腥爪击 AND 能够刷新斜掠流血DOT）OR {有血腥爪击buff AND [（没有丛林之魂天赋 AND 斜掠流血DOT可持续时间小于9秒）OR 斜掠流血DOT可持续时间小于6秒] AND *FeralBleedSnapshot*大于 RakeBuffs的伤害峰值除以2} OR 有影遁buff】 AND 目标预计死亡时间大于斜掠流血总可持续时间除以2

	释放 斜掠

3. if 【没有斜掠DOT OR （ 没有血腥爪击天赋 AND 能刷新斜掠流血DOT） OR {有血腥爪击buff AND [（没有有丛林之魂天赋 AND 斜掠DOT可持续时间小于9秒） OR 斜掠DOT可持续小于6秒]} AND *FeralBleedSnapshot*大于 RakeBuffs的伤害峰值除以2】AND 目标预计死亡时间大于斜掠流血总可持续时间除以2 AND 横扫可命中敌人大于1

	释放 斜掠（此时为多目标模式，最多3个）
4. if 能量大于等于释放斜掠的能量 AND [（野蛮挥砍得充能层数大于等于2 AND 野蛮挥砍的下一层充能时间小于等于GCD）OR 野蛮挥砍可命中目标大于1 OR 目标预计死亡时间 小于 野蛮挥砍目前可使用的层数乘以野蛮挥砍的总体冷却时间]

	释放 野蛮挥砍
5. if 能够刷新月火术DOT AND 有斜掠DOT AND 目标预计死亡时间大于10秒

	释放 月火术（此时为多目标模式，最多5个）
6. if 痛击可命中敌人数目大于等于3 AND 可以刷新痛击流血DOT

	释放 痛击
7. if 横扫可命中敌人数目大于等于3 AND 可以刷新横扫流血DOT

	释放 横扫
8. if 横扫可命中敌人数目小于3

	释放 撕碎
***
===

*定义*  **Cooldowns** ACTION

1. 使用饰品
2. 使用种族技能

***
===

*解释*  **FeralBleedSnapshot** 变量

其值等于

= (1 + 有猛虎之怒buff赋值1，没有赋值0) 乘以 (1 + 有野蛮咆哮buff赋值1，没有0) 乘以 (1 + 有血腥爪击赋值1，没有0)

*解释*  **RipBuffs** 变量

其值等于

= 割裂释放消耗的连击点数 乘以 (1 + 神器特质锋锐利齿层数 * 0.07) 乘以 **FeralBleedSnapshot**

*解释*  **RakeBuffs** 变量

其值等于

= **FeralBleedSnapshot**

但是如果 有潜行buff OR 有化身：丛林之王buff or 有影遁buff
   = **FeralBleedSnapshot** * 2