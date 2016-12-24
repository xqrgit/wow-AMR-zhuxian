AMR战斗历程
==
暗牧 （含自杀牧逻辑）
==
>http://www.askmrrobot.com/wow/theory/rotation/amrpriestshadowdefault?spec=PriestShadow&version=live

>源文件

***
###名词解释
`VF S2M 都是开关`
`S2MStartTime 是个变量 需要一个函数进行计算，附在后面`
***

1. 执行 暗影形态
2. if 在虚空爆发形态中 AND 没有开启疯入膏肓  **VF** 开关打开

	if 不在虚空爆发形态中 **VF** 开关关闭
3. if 有疯入膏肓buff **S2M** 开关打开

	if 没有疯入膏肓buff **S2M** 开关关闭
	
	>此开关为后面做准备，貌似没啥大用
4. 执行 嗜血
5. if 目标预计死亡时间 小于 **S2MStartTime** AND 虚空形态的层数小于5层 AND 虚空爆发已经结束 AND BOSS血量小于1%（这是AMR的逻辑，我有点不太理解，但还是照实翻译）
 
	执行 疯入膏肓
6. if 有虚空爆发buff 

	进入 *InVoidForm* ACTION
	>此action会在后面解释
7. 执行 摧心魔
8. if 吸血鬼之触DOT可刷新 AND 可以释放 虚空爆发 
	
	执行吸血鬼之触
	>dot可刷新的意思是 30%rule 就是dot持续时间小于dot总时间的30%
9. if 暗言术：痛dot可刷新 AND 可以释放 虚空爆发

	执行 暗言术：痛
10. if 没有点上 疯入膏肓 天赋
	执行 虚空爆发
11. if 点出了 疯入膏肓 天赋 AND [有战败之魂buff OR 目标预计死亡时间 大于 **S2MStartTime** + 虚空爆发平均持续时间]
>在这里如果想确定一个非常准确的虚空爆发平均持续时间 需要设一个变量一直在记录，然后取平均，如果不想那么麻烦，各位可以自行设置
12. 执行 暗影冲撞
13. if 目标们的距离你大于1码 AND 可以刷新吸血鬼之触DOT 目标预计死亡时间大于6秒 AND 天赋撒莱茵点出来了

	 执行 吸血鬼之触 （此时为多目标模式，一直寻找周围满足条件的目标，给周围最多5个目标保持此DOT，一旦找到，给他上了触，马上需要切换回原目标）
14. if 目标们距离你大于1码 AND 可以刷新痛的DOT AND 目标预计死亡时间大于4秒 AND 有痛DOT的目标个数小于等于有触的目标个数

	执行 暗言术：痛 （此时为多目标模式，同上，最多给4个上。IF 天赋吉兆点了出来，最多给5个上）
15. if 目标们距离你大于1码 AND 可以刷新触DOT AND 目标预计死亡时间大于6秒

	执行 吸血鬼之触 （此时为多目标模式，最多5个）
16. if 目标们距离你大于1码 AND 可以刷新痛DOT AND 目标预计死亡时间大于4秒 AND 天赋吉兆点出来了

	执行 暗言术：痛 （此时为多目标模式，最多8个）
17. if 精神灼烧可以烧到4个及以上目标

	执行 精神灼烧 （注意，如果可以使用虚空爆发，随时打断此法术）
18. 执行 暗言术：灭
19. if 目前心灵震爆层数等于最大心灵震爆层数 OR [目前心灵震爆层数大于等于 最大心灵震爆层数-1 AND 天赋暗影洞察已点出来了]
>Mangaza's Madness gives Mind Blast 3 charges, so this logic is to make the most use of that legendary. Without it, this just casts Mind Blast on cooldown. With it, you want to always cast at max charges, cast with 2 or 3 charges if you have Shadowy Insight, otherwise save the charges for Voidform.暗牧橙腰带心灵震爆可以最大3层，此逻辑为了最大化优势。如果没有橙，老老实实心灵震爆冷却好就用。如果有了橙，如果你点出暗影洞察来了，可以2层或者3层放心灵震爆，如果没点出来，留着给虚空爆发。
20. if 可以刷新痛DOT AND 目标预计死亡时间大于4秒

	执行 暗言术：痛
21. if 可以刷新触DOT AND 目标预计死亡时间大于6秒

	执行 触
22. if 暗言术：虚的当前层数等于最大层数

	执行 暗言术：虚
23. 执行 心灵尖刺
24. 执行 精神鞭笞（优先级很低，随时可以打断）

=====================
***
定义 *InVoidForm* ACTION
>这就是前面第六步那个 如果在泰坦里，可以新建一个action，然后当上面那个主要循环满足了条件，直接return到此action，此时为角色进入虚空爆发

1. 开启爆发

	使用饰品
	
	使用兽人种族技能 if [没有战败之魂buff AND 虚空形态的层数大于15] OR 有战败之魂buff AND 目标预计死亡时间小于30秒
	
	使用巨魔种族技能 if 没有嗜血buff AND 没有能量灌注buff
2. 执行 虚空箭
3. if 有战败之魂buff AND 触的可持续时间大于引导虚空洪流时间+虚空箭到达目标的时间 AND 痛的可持续时间大于引导虚空洪流时间+虚空箭到达目标的时间

	执行 虚空洪流
4. if 没有战败之魂buff AND 没有嗜血buff AND [天赋疯入膏肓没有点出来 OR 目标预计死亡时间大于**S2MStartTime**+虚空洪流冷却时间]

	执行 虚空洪流
5. if 有战败之魂buff AND 上一个技能是虚空箭 AND 疯入膏肓冷却时间大于540秒 AND **S2MStartTime** 大于等于115秒

	执行 消散
	>此消散为刚开自杀用一次，以延长总体时间
6. if 有战败之魂buff AND {[狂乱每秒减少的值乘以（GCD+0.25秒）]大于当前的狂乱值}

	执行 消散
	>注意如果此时用regen的函数的话，会return一个负值，注意取绝对值；同时此消散的逻辑是马上跌出虚空形态了，并且没有技能可以放，用个消散来等冷却
7. 执行 暗影冲撞
8. if 上一个技能是虚空箭 AND 狂乱值小于80 

	执行 摧心魔
9. if 有战败之魂buff AND 虚空形态的层数 大于 0.7乘以虚空爆发平均持续时间（参考上面第11步）

	执行 能量灌注
10. if [虚空形态层数 大于 虚空爆发平均持续时间-能量灌注的总可持续时间-5] AND [自杀天赋没点出来 OR 目标预计死亡时间大于 0.3乘以虚空爆发平均持续时间+能量灌注冷却时间]

	执行 能量灌注
11. if 没有战败之魂buff OR {有战败之魂buff AND 天赋夺魂之镰点出来了 AND [狂乱每秒减少的值乘以（GCD+0.25秒）]大于当前的狂乱值}

	执行 暗言术：灭 
	>此逻辑为留一个灭防止突然掉出虚空形态而猝死
12. if （狂乱每秒减少的值乘以GCD）大于当前的狂乱值

	执行 奥术洪流
13. if 有战败之魂buff AND 狂乱缺少值大于（50-狂乱每秒减少的值乘以GCD）
14. if 目标们距离你大于1码 AND 可以刷新痛的DOT AND 目标预计死亡时间大于4秒 AND 有痛DOT的目标个数小于等于有触的目标个数

	执行 暗言术：痛 （此时为多目标模式，最多给4个上）
15. if 目标们的距离你大于1码 AND 可以刷新吸血鬼之触DOT 目标预计死亡时间大于6秒

	 执行 吸血鬼之触 （此时为多目标模式，给周围最多4个）
16. if 精神灼烧可以攻击到的目标数目大于等于4
	
	执行 精神灼烧 （一旦可以用虚空箭或者灼烧目标小于4个，马上打断）
17. if 有暗影洞察的buff可以瞬发震爆 OR （上一个法术不是精神鞭笞 AND 上一个法术不是心灵尖刺）

	执行 心灵震爆
18.  if 当前灭的层数=最大层数

	执行 暗言术：灭
19. if （没有战败之魂buff AND 虚空形态层数大于15层） OR （有战败之魂buff AND 虚空形态层数大于60层）

	执行 暗影魔
20. if 痛DOT可持续时间小于（虚空箭冷却时间+虚空箭到达目标时间） AND 目标预计死亡时间大于4秒

	执行 痛
21. if 触DOT可持续时间小于（虚空箭冷却时间+虚空箭到达目标时间） AND 目标预计死亡时间大于6秒

	执行 触
22. if 精神灼烧可命中目标大于等于3 AND [虚空箭冷却时间大于 1除以(1+总急速)] AND [心灵震爆冷却时间大于 1除以（1+总急速）]

	执行 精神灼烧
23. 执行 心灵尖刺
24. 执行 精神鞭笞 别的一旦满足，随时可以打断

====
***
###解释 S2MStartTime 变量
此变量的值为
>前提条件 赋值
>
>hasteIndex = Min(急速值, 12000) / 3000
>
>critIndex = Min(暴击值, 12000) / 3000

>haste1 = Floor(急速指数) + 1

>haste2 = Ceiling(急速指数) + 1

>crit1 = 0

>crit2 = 0

if 天赋吉兆点出来了 then crit1 = Floor(critIndex)

if 天赋吉兆点出来了 then crit2 = Ceiling(critIndex)

if 急速值大于等于 6000 AND 小于 9000 then haste1=haste2

critValue1 = SurrenderStartValues(haste1,crit1) + ((SurrenderStartValues(haste1,crit2) - SurrenderStartValues(haste1,crit1)) * (critIndex - crit1))

critVal2 = SurrenderStartValues(haste2,crit1) + ((SurrenderStartValues(haste2,crit2) - SurrenderStartValues(haste2,crit1)) * (critIndex - crit1))

	注意，这里SurrenderStartValues为Lua数组，数组的DATA为
	{
	  "1": "[102.5,105,107.5,108.75,110]",
	  "2": "[107.5,108.75,110,112.5,114]",
	  "3": "[112.5,112.5,112.5,114,114]", 
	  "4": "[115,117.5,125,130,132.5]", 
	  "5": "[120,125,130,132.5,135]"  
	}

S2MStartTime 的 Result = critVal1 + ((critVal2 - critVal1) * (hasteIndex - (haste1 - 1)))

if 没有夺魂之镰天赋 AND 急速值大于等于7500

Result=Result - 22.5
	
if 没有夺魂之镰天赋 AND 急速值小于7500

Result = Result - 15

if 没有能量灌注天赋

Result = Result - 10

if 有意志壁垒天赋

Result = Result + 5

if 有暗言术虚天赋

Result = Result + 2.5

if Result 小于 90 then Result = 90

if 有暗牧橙腰带 then mangazasMod = 0

if 急速值小于9000 AND 有橙腰带

mangazasMod = mangazasMod + Max((haste1 - 2) * 2.5, 0)

if 急速值大于等于9000 AND 有腰带

mangazasMod = mangazasMod + (haste1 - 1) * 2.5

if 有腰带 AND 有暗影洞察天赋

mangazasMod = mangazasMod * 2

if 有腰带 then 

Result = Result + mangazasMod

if 有腰带 AND Result 大于等于115 AND 急速小于9000

Result = Result + 15

if 嗜血CD时间大于0 OR 总体战斗秒数乘以0.3 小于 55秒

Result = Result - 7.5

if （嗜血CD时间大于0 OR 总体战斗秒数乘以0.3 小于 55秒） AND 急速值大于6000

Result = Result - (急速值 - 6000) / 6000 * 12.5)
>注意这个总体战斗时间是从一开始战斗到目标死亡的总体时间

if （嗜血CD时间大于0 OR 总体战斗秒数乘以0.3 小于 55秒） AND 急速值大于6000 AND Result 大于等于115

Result = Result - 5

if 有橙腰带 AND 总体战斗时间大于等于Result + 虚空爆发平均持续时间

Result = Result + 2.5