<!-- 商家销量统计的横向柱状图 -->
<template>
  <div class="com-container">
    <div class="com-chart" ref="brand_bar_ref"></div>
    <span class="iconfont arr-left" @click="toLeft" :style="comStyle">&#xe6ef;</span>
    <span class="iconfont arr-right" @click="toRight" :style="comStyle">&#xe6ed;</span>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import { getThemeValue } from '@/utils/theme_utils'
export default {
  data () {
    return {
      chartInstance: null,
      allData: {
        sellerNames: ['喜莱卡旗舰店', '臭皮匠家居旗舰店', '捷花旗舰店', '神涎家居旗舰店', '荷叶堂旗舰店', '南十字星旗舰店', '红遍天家居旗舰店', '言信花厂', '格帆植物', '锦上添花20140728', '西湖碟花卉旗舰店', '牛郎织女旗舰店', '街心公园旗舰店', '如一花开旗舰店', '诚艺家居旗舰店', '苗乐乐花坊', '美饰每客旗舰店', 'a275756517', '森仕旗舰店', '乡青绿植工厂', '泰环旗舰店', '森泰家居旗舰店', '百花记旗舰店', '花咖flower', '鑫啸绿植', 'wyzdyzcfy', '恋柚旗舰店', '凉笙家居旗舰店', '八点好奇心', '初平旗舰店', '蝶舞花坊v', '罗曼园艺', '水之清心之净', '鑫啸旗舰店', '醒木家居用品旗舰店', 'artizanmoss', '天云海蓝旗舰店', '馨茹花坊', '仙豆花艺', '陌卡花艺', '滨客家居旗舰店', '风过南国', '木木浩1972', 'qq为爱变乖', '花千韵植物', '拉唯丽', '义乌市昭彩纸盒厂1', '致本家居旗舰店', 'willon2007', '绿跃仿真植物', '夕夕美屋旗舰店', '晨橙旗舰店', '掬涵旗舰店', 'hdh旗舰店', '花常红', '满庭芳花艺有限公司', '在野家居旗舰店', '珀姿曼旗舰店', '法璐奇旗舰店', '空净旗舰店', '李阳whxbtdz', '糖果星期八', '简菊旗舰店', '在野软装花艺设计', 'a_忘忧草_a', '花墙花巷', '绿杨旗舰店', '雨麦旗舰店', '陌本家居旗舰店', '想容的猫窝', '爱泽宝家居旗舰店', '义乌市燕舞工艺品', '左岸麦田旗舰店', '36232519870901122x', '绿道旗舰店', '美歌伦旗舰店', '刺青1525796', '润野花卉', '布意坊687', '态_生活馆', '12嘎飞12', '江自葵', 'pyy068', 'songgenshen55', '润野旗舰店', '贝汉美家居旗舰店', 'lolita小绿', '微云家居商城', '花族旗舰店', 'driftbottle漂流瓶旗舰店', '陌歌旗舰店', '三唯一居旗舰店', '娅莉娜旗舰店', '相逢9999', 'evemei伊芙美旗舰店', '莱雅花艺旗舰店', '毛菇小象恋恋衣舍', '爱丽达家居旗舰店', '名仕情怀', '花与梦旗舰店', '美伊朵旗舰店', '一把伞1991', 'wonbly', '花格一间旗舰店', '蓦然88回首', '武德鼎', 'wojia家居旗舰店', '原野家居旗舰店', '知根旗舰店', '往红旗舰店', '尔恩娜芙旗舰店', '花爵士旗舰店', '红艺坊家居生活馆', '个性花季旗舰店', '糖果星期八旗舰店', '保佑我的宝', '农夫水田', '黑妹00', 'kailisiky', '五瓣丁香旗舰店', '创业梦工场8888', '天熠林工艺绢花厂', '6dushop', '顾居家居旗舰店', '初衷旗舰店', '让鑫花艺', '芷晶城旗舰店', '惊涛king', '绘雅旗舰店', '热情喂给风l', '罗曼妈妈家居旗舰店', '西西花艺1号店', '绿跃旗舰店', 'lyhxkj8', 'ladylike栀美家家居旗舰店', '争艳花艺1138', 'suzhaoyang_2009', '谷灵易生旗舰店', '花草堂家居旗舰店', '格兰蒙旗舰店', '春在原野1', '香蒲玫瑰批发', '小裁缝阿烫', '森绿园艺有限公司', '卢浮宫旗舰店', '文苑花卉旗舰店', '跳跳的囡囡', '我离五百万差一步', '家中有花企业店', '抖冉旗舰店', '光影艺轩旗舰店', '星期八精品服饰', '郭冰214445279', '画朵工艺', 'bonnardic', '最是少女', '苏锦绿植旗舰店', '香环旗舰店', 'tb7860605174', '金祥源旗舰店', '花之韵家居旗舰店', '豪匠花卉旗舰店', 'si294128263', '欧城旗舰店', '亭亭玉绿', 'euk旗舰店', '佑尚精品之家', '格调印象旗舰店', '采薇花艺旗舰店', '北京云港家具', '琉璃岛旗舰店', '花弄影_花艺', '嘉和饰欣旗舰店', '四月花坊旗舰店', '雨轩的未来', '法兰克福风情2010', '张锐佳88', '诗萱儿旗舰店', 'zjywwhb', '繁花仙子旗舰店', '0mall', '瑰姿艳逸家居旗舰店', '沐色拾光', '星尘旗舰店', '宇洁花艺', '钧月窑家居旗舰店', '漫果旗舰店', '朝熙家居旗舰店', 'dl婚庆花艺', '博艺达园艺旗舰店', '香茗源旗舰店', '美美美家居', '宜兰旗舰店', '蔷薇花开旗舰店', 'tb5061503543', 'ikea宜家家居官方旗舰店', '宇洋无垠', '枫爱旗舰店', '半壁倾城s', 'chuanchuanfa', '味精说', '摩屋家饰旗舰店', '1张建静11', '蝶_恋黄昏', 't_black', '千居阁1688', 'ueraydy家居旗舰店', '彩乐滋旗舰店', '御三泥旗舰店', '飘亮旗舰店', '美千耀8898', '优贝家旗舰店', 'miz米子家居旗舰店', '蒋萌11', '243915870xm', 'xuzhenzhen1224', '加芬美饰旗舰店', '大睿花坊', '慕春旗舰店', '乐美花艺', '百永花坊', '艾芙朵旗舰店', 'wks624', '鱼西美屋杂货铺旗舰', '星怡婚庆旗舰店', 'jinpin0227', '古索绿植旗舰店', '红绣罗达旗舰店', '天姿花坊', '虫insect', '鑫工艺1', '雅昀家居专营店', '网通狂', '俯瞰大地gg', 'zhizhuo蜘蛛', '玐玖琦珥旗舰店', 'xlzhhhyn', '倾绿坊植物', '满庭芳家居用品旗舰店', '梦泓尧家居旗舰店', '高哲920916', '趁现在就购了', 'meikeda5201314', '新蒸旗舰店', '艺枝秀', '李梓硕518', '清雅服饰', 'ks家居旗舰', '爱之果家居旗舰店', '购巴园艺场', '趴趴轰', 'liuchao6010', '毛小熊的春天', '独秀家林旗舰店', 'zhugexuran', '忠歌旗舰店', '艺雅轩家居旗舰店', '翻旧事旗舰店', '奕媚旗舰店', '格润家居用品专营店', 'wlxzh20100', '文轩工艺干花', '艺帮手旗舰店', '朴记旗舰店', '恋之艺家居旗舰店', 'judyzhang514', '了咯哈柯尼卡', '映菡旗舰店', '千意家居用品旗舰店', '汪莉蔓芊花艺', '静听花落谁家', 'clq不老泉_源', '森琳旗舰店', 't_1491040902882_0394', 'xiaofantuanxing', 'livetai旗舰店', '皓杨家居旗舰店', '陶度旗舰店', '波浪湾旗舰店', '范丹阳11', 'rl潘潘潘', 'flowerwall旗舰店', 'taoqi1017', 'xingsheng105', '和家的芳草园', 'zgwzzxz', '泽熙花艺', '初晨初梦专卖店', 'chenruoxi1992', '拾忆家居旗舰店', '欢欢hyl', '百花奇缘花房', '竹子批发市场', '蝶爱旗舰店', '家骆花艺馆', 'linminhjua', '欧阳19900625', '2009钧钧', '520等你好久', '华美达家居旗舰店', '妙绿旗舰店', '素年锦时旗舰店', 'chenxi19870616', '懒人学堂旗舰店', '忆香家居旗舰店', 'tb3933845823', 'zaq12_2005', '绿然装饰001', '花王企业店铺', '唐朝家居旗舰店', '天眷旗舰店', '美象旗舰店', '叶脉花的国度', 'bestwest旗舰店', '轩晓彤旗舰店', 'happybear小乐熊旗舰店', '印象80艺馆旗舰店', '美天地花艺无锡店', '董先森a', '红萱旗舰店', '优鲜森旗舰店', '好品源瓷器厂家店', 'wunvshi01', '谷灵家居旗舰店', '胖宝宝丶哒', '花之语花艺馆', 'qq13791972775', '竹暄旗舰店', '颂思缘旗舰店', '图迈生活美家', '陌仟花艺', 'qq342333679', '天之小宇', '糖糖19920613', 'luoxiaotie123', '简体汉文', '吴彦燚', '谜森旗舰店', '兵哥哥创业梦', '北木花艺生活馆', '图略旗舰店', '麦桐旗舰店', '对角线0406', '晨惜工艺花坊', '环海一号', '迷妆旗舰店', '长耳朵的驴子', '绿野阳光旗舰店', '颜忆旗舰店', '美宜空间家居旗舰店', '晶华旗舰店', '遥望此处花满楼', '瓷韵阁家居', '花儿朵朵13144', '森艺诚', '大田屋山下', '西西里旗舰店', 'markyim80', '浩情旗舰店', '满天星家居旗舰店', 'yong596706983', '幸福之家971122', '姜子烨', 'vivi淘淘淘', '四季花开家饰', '朵馨旗舰店', '每束旗舰店', '筑业家居旗舰店', 'tb413856834', '艺岚园艺旗舰店', '与优与美旗舰店', '承诺一张纸1', '贵州展飞酒业', '银杏树花艺', '明扬机械88', '蝶衣恋儿', '英伦欧堡旗舰店', '雨林工艺坊', 'coolercolour', 'leonn101', 'zhaiheng', '大艾绿植旗舰店', '欧莱特家居旗舰店', '二小宝旗舰店', '悯戌旗舰店', '纳茉旗舰店', '缘起今生花卉', '花花世界花卉馆', '巧农家旗舰店', '小花杂货铺丫', 'yk何强', '翻旧事聚合专卖店', '世茂园林', '追忆旗舰店', '郁香菲家居旗舰店', '叹息的肉丸子', '晶华造花', '梦渃旗舰店', 'oknana', '万家仓', 'kuerpy旗舰店', 'ljw咖啡加茶', '胡美晨的店', '琪彦乐淘', '魅影时尚x', 'lichunyann', 'a414151988', '枷锁7703', 'tb652814197', '欧布妮旗舰店', '西尚玫瑰家居旗舰店', '艺品嘉艺', '童年再美终究是回忆', '缘印旗舰店', '艺家艺雕刻工艺', 'dt是个妞', '初见家饰品牌店', '瑰蕾旗舰店', '蔓眉旗舰店', 'swerlem', '伊丽雅佳旗舰店', '纪美旗舰店', '赢岛臻绿旗舰店', '阑珊树旗舰店', 'wangyuhua2009', '六月小老虎', '紫藤工艺店', 'hzmgw', '大傅旗舰店', '杜二方22', '花卉人生旗舰店', '丹桂苑旗舰店', '昶晟旗舰店', '植之悟', '花九歌旗舰店', '黄氏万木枋', '冰石美旗舰店', 'rjonwu', '刘玲玲123456789562301974', '双影礼品屋', '江苏大自然园林', '清汤卧果旗舰店', '四季花海旗舰店', '睿智则心静666', '精品花都', '艺露旗舰店', 'wangxiaos456', '春山艺术', '礼赫家饰品牌店', '梵原花艺工作室', '虾公公41', '新丝维服饰', '林薇花卉', '吾喜欢的', '80后花坊', '茜云旗舰店', '野花花卉旗舰店', '1993梦梦00', '紫玉成烟家居旗舰店', 'yuangwang7475491', '至诚至爱家居旗舰店', 'chen226310', 'xiaotangguo0103', '赛安娜旗舰店', '喜韶旗舰店', '童伟琴134', '沁花轩', '田野百花园', 'xingxing19820928', '独秀家林1', '玉华阁玉器商城', 'wtiantiana', '梦婷19911016', '168chunxia', '中国红喜铺掌柜', '悄悄qqq', '绚懿华旭专卖店', '东驰旗舰店', '桫梅卡高端仿真园艺', '罗紫云shine', '专业印刷五十年', '霍夫特洛夫斯基', '龙哥仔20537207', 'w彤彤baby', '家之炫旗舰店', '义乌鑫鹏塑料花', '优讯旗舰店', '朝阳尚品馆', '陌上花开336', 'allen_770', 'miyulife', '圣西罗6677', '薛大治', 'tb4988996_00', '小坏光', '121im5', '义乌小商品5', '弦姑娘', '诺凡居言旗舰店', '五姐弟家居旗舰店', '七彩图旗舰店', '尚饰界家居旗舰店', '欧裔家居旗舰店', 'harborhouse家居店', '琉璃兰旗舰店', '创意礼品坊旗舰店', '蜜蜂小姐旗舰店', '毕振欢刘春灵', '刘艳娟911', '摩品家居旗舰店', 'abc小囡囡', 'tb043737564', '小白菜的花', '茗博坊陶瓷有限公司', '鼎泓建筑', '呼噜妹366', '汇景园花坊', '海虹雅林旗舰店', '茂朵旗舰店', '云裳407157250', 'richdeer箱包', '汪声满园旗舰店', '美学黑客旗舰店', '1鸩羽千夜l', '千百度家饰', '在景轩花阁', '温馨花坊企业店', '飞雪家居专营店', '笑笑1620', '添上美0', '猫兜公主', '蒂莎旗舰店', '通通摄影道具', '俏爱旗舰店', '当然是因为喜欢啦', '朗世达实创专卖店', '私家时尚馆', 'tb601767828', '恋尚花家居旗舰店', '喜羊羊工艺', '梁栋allan', '常青旋律', 'ygqt旗舰店', '朗怡旗舰店', '瑞丽家居专营店', '龙龙238843', '天熠林旗舰店', '程莱旗舰店', 'tb16553228', 'tb1756756_2011', 'xbgracexf99', 'yzshanghaihaihong', '初若安然旗舰店', '嗨借个微笑呗520', '满城花家居旗舰店', 'jie19912009', 'lyt20120618', 'yuyue19891214', '微饰界旗舰店', '植世子旗舰店', '浪漫之都2110', '爱尚花', 'aihaishang888', '蓝色宁静wuyuan', '丽贝娜旗舰店', '奇居良品家居旗舰店', '春绸旗舰店', '爱的诺言19861024', '娜恋家', '暖暖婕', '绚懿轩宇专卖店', 'tb_875433', '慕风居旗舰店', '老婆好a', '鸡年好运到', 'xiaomao1688', '七色花艺店', '墨染留香家居旗舰店', '朵兰舍旗舰店', '爱尚易家', '红尘家居专营店', 'luowentong', '美好花艺520', 'tb6917282', '三春三夏旗舰店', '摩登_格调', '米子花阁', '蜜萝丽旗舰店', '布施贝旗舰店', '幸福满屋899', '慕言旗舰店', '美兰饰家软装花艺厂家店', '景鼎家居旗舰店', '暗香花艺生活馆', '橡树庄园旗舰店', '邦德花艺', 'yyu20102', '宇恩旗舰店', '果丽维意旗舰店', '樱舞花艺', '百合花开19897', '风丶之殇', '一悦旗舰店', '悠然花香之家', '皇家森林旗舰店', 'tb803989008', '商务原创花艺', '灵彩家居旗舰店', 'ali662720146', '时光巴士旗舰店', '绿茵植物店', 'linli202', 'zisemenghun', '初晨家居旗舰店', '夏梵旗舰店', 'abundantsource', 'mweiweilove', '万众笑旗舰店', '义乌市奕博工艺品有限公司', '比美工艺品', '皮皮水园艺旗舰店', '花思木旗舰店', 'jp集品空间', '夏春红25', '雨婷化妆品商贸', 'jbv旗舰店', '小丝恋', '昊锦旗舰店', '花无情家居旗舰店', '花涧田舍旗舰店', 'janelove旗舰店', '微世界家居装饰', '方先森gg', '花伴伊生旗舰店', '香彩旗舰店', 'husitiao', '清香四溢花园', '爱伦黛尔旗舰店', 'czk588', 'funny齐刘海', 'yuhui20090405', '东霆旗舰店', '松果的店', '流金海岸旗舰店', 'tb039540890', '小曹子193', '豆磨家旗舰店', '锐志集团', '鹏杨花艺', '花梦谷旗舰店', '霞霞娃', 'zhouminxiaolou', '上品2号馆', '专属天使家居用品旗舰店', '丝蒂琦小屋', '欧可莱旗舰店', '花落谁家家居旗舰店', '京开花业', '鑫艺尚火锅用品', 'bossihomechina', 'fashion慕溪', '大腕旗舰店', '碧海青天08760799', '花邻堡旗舰店', '镧林家居旗舰店', 'daxixikeji', 'tb741888152', '卢红亮1983', '安蒂服饰', '星星不遥远', '艺陶千年旗舰店', '萌家仿真花制造厂', 'amsffgmy', '小燕子园艺', '巢派旗舰店', '本与bunyum', '阳光屋花艺', '米拉迪旗舰店', 'chenmian151', 'tb822316076', '东来家居软装', '京卉旗舰店', '伊人依斋', '可爱小考拉', '大鹏工艺品858', '志康家居专营店', '波黎大方家居专营店', '金丝南园', 'linyanjun401', 'pgr6842681', 'yuanlei2076', 'zhangxueliang1236', '宁雪儿旗舰店', '小猪猪泽品专卖店', '温馨花艺82', '笑看人生19787', 'x1998yj', '峰景家居旗舰店', '果果家坊', '东方姑娘品牌店', '凤头鹰旗舰店', '孙茂晨2012', '木英四月三', '美嘉博旗舰店', 'kawslll1', 'ly252024000', '型xiao佳177', '尚居家居旗舰店', '紫香凝旗舰店', 'tb22610444', '俏晶豆旗舰店', '六点零七分', '帕妮莎旗舰店', '花语仿真植物工厂', '远兮旗舰店', '馥郁旗舰店', 'l307841292', 'tb205662_55', '侯长征65318005', '卡洛花饰', '川久的店', '百花争艳品牌店', '眉益旗舰店', '露巧旗舰店', 'babyblue_r', 'tb229852125', '吉祥园_2008', '蓝皮鼠家居旗舰店', '常菁园', '泥人制造', '烈在岛', '皇贺旗舰店', '花舍家居旗舰店', '鸿发园艺设计制作中心', '001装饰工艺品', 'smiling李丹', '凌峰旗舰店', '山东朵朵花艺', '帝伯尼商贸', '百草集12138', '花芝语花坊', '西西的九毛', '123玉红123', '8819微笑', 'viola_lee_81', '中萃园林绿化有限公司', '优可都旗舰店', '创异工社', '洪梦华', '演绎角戏', '路边那条野狗', '雪辉陈年如月', '不见了青蛙', '小小小雨l', '秋秋爱坑吭', '臻久家居旗舰店', '艺贝子家居旗舰店', '饰趣旗舰店', '俪锦旗舰店', '刘秀娟_1986', '千叶创生活', '孤岛三哥', '泥无界旗舰店', '香香洋洋祥祥', 'ying_zhijia', '宁微旗舰店', '微微笑笑即倾城', '艺宝格家居旗舰店', '贵州苗家铺子', '高木木0929', '大菜头888', '希露思旗舰店', '柔媚青春', '汉唐国风家居专营店', 'xiaoyibang88', '十年花艺', '张鹤0427', '花先花生', '晴雨季花艺', '柳趣旗舰店', '树有专功园艺', '梅花艺品', '筱筱最坏', '花香四溢hxl', '贝朵拉旗舰店', '香朵儿饰品旗舰店', 'dadio搭调旗舰店', 'huayihome', 'mazhaoping18888', 'tb2916415516', '农耕山旗舰店', '博艺坊旗舰店', '大块渔旗舰店', '李赛球', '松雨旗舰店', '闽泉家居旗舰店', 'nfzhong_2011', 't_1491231979349_0456', '婵娟绿植旗舰店', '朗世达天下居专卖店', '美艺坊软装批发', '花儿or叶儿', 'tb7213582348', '三春三夏家装', '初见初梦专卖店', '恒尔玛旗舰店', '江扬高邮', '生活饰界2008', '白菜2528524', '夏岩园艺旗舰店', '来来去去8891', '梦飞服饰5905', '瑰蕾花艺', '纯情小火鸡丶', '花点空间', '茱丽叶miss', '吸着香烟的帅小伙', '宝贝儿妈妈1688', '时尚宝贝我爱你99', 'alienchou1991', 'lirong1256', 'sunbo18218020158', 'tb361957237', '华盈旗舰店', '原林花艺', '墨一家居旗舰店', '序强旗舰店', '恋想小屋', '柏以凡旗舰店', '爱蒂可家居专营店', '风华绝代家居饰品', '马炎溪', '1步两个鞋印', 'zh19861215', '云霄花坊', '我喜欢我最棒', '花卉世家1217', '苑广东', '藤格先生家居旗舰店', '金鹭鲤旗舰店', 'jjq915044', 'xiong0535', '天天笔业111', '婴特旗舰店', '晟煊旗舰店', '歌优比旗舰店', '正想旗舰店', '淼乐家居专营店', '绚懿永邦专卖店', 'sczltangtang1234', 'tb7577704', '凯旋花卉园艺场', '卡洛琪旗舰店', '山峰之巅66688', '艺品花舍888', 'cocototo1985', 'cute_girl616', 'cx2464075904', 'xiaobeibeimei', '宝云制花', '怡贝贝7758', 'huayutang88', 'shqssyyxgs', '凸出旗舰店', '常相思花卉园艺', '栀子花开春夏秋冬', '琢彩旗舰店', '芭蒂旗舰店', 'jie292699024', '奕昱汐服饰旗舰店', '杨小颖567', '清枫苑家居旗舰店', '点睛之笔园艺', '福泽林旗舰店', '秋语花卉旗舰店', '第一朵玫瑰连锁花店', '纤蜜莉旗舰店', 'guige2009', 'zairenjianchen', '又长胖了8斤', '图迈生活美学馆', '成都芙蓉花店55', '旺丁旺财家居专营店', '森埠旗舰店', '熙曼蒂旗舰店', '芦汉芦汉', '阿伟111', '阿山哥xdx', 'chou毛', 'fan01987', 'zoulongqiao', '伽亿旗舰店', '君志旗舰店', '墨菲家居旗舰店', '大姐花店', '桃子宝贝304', '森艺诚旗舰店', '疏桐雨', '米图软装生活馆', '美兰饰家', '美空旗舰店', '腾美家居专营店', '薇娇旗舰店', '飞谍旗舰店', '89笨小孩', 'rehome旗舰店', 'tao家居旗舰店', 'tb304404632', '允畅旗舰店', '君凯陶瓷旗舰店', '如意乐法淘淘', '念源旗舰店', '欧月家居专营店', '禹涵旗舰店', '花枝艺园', '苏墨家居旗舰店', '荣词旗舰店', '鎏玉堂旗舰店', 'as1273216657', 'essey旗舰店', 'pm1314925', 'tb173636934', '亿人制袋', '假猪套天下第一468', '咕噜咕噜海贼王', '姜慧霞1987', '左八斤att', '愚心旗舰店', '试试鞋', 'iikizeng', 'tb386474874', 'vip锲而不舍', '植富园', '泊盛旗舰店', '美馨美妍', '艺饰家企业', '鱼饰旗舰店', 't_1492878838997_0187', '仙思图家居旗舰店', '地主154042296', '子佳工艺', '宠格旗舰店', '寻爱旗舰店', '平价买卖商店', '悦馨旗舰店', '贝汉美颜忆专卖店', '钩钩坊', '骆雪家居旗舰店', 'starryfeng518', '五妹子花厂', '兰亭翰明专卖店', '凯恩斯家居旗舰店', '庆缘景观旗舰店', '庆铎旗舰店', '快润发旗舰店', '格诗美旗舰店', '童心树旗舰店', '艺绘旗舰店', '蒂拉旗舰店', 'firstlove旗舰店', '古戴旗舰店', '粒子世家', '美丽网购小屋', '藤艺家居小屋', '踏遍天下460935286', '伽马旗舰店', '农家春旗舰店', '嘉茹旗舰店', '蘑菇街旗下品牌', 'tb938776314', 'w42137196', '全齐电商导航仪', '华兴亿丰企业店', '弓矢有品旗舰店', '杨秋峰55', '桥头金之冠', '淘花阁98', '米琪妃旗舰店', '美美哒家居店', '诚信咕噜圃', '轩辕家居旗舰店', 'shujingrong', '串串cc8', '初见家居旗舰店', '喜力美旗舰店', '朝聚旗舰店', '果养你旗舰店', '花妖媚旗舰店', '誉帝饰品旗舰店', '谁要比我惨', 'lx6666', 'pan103201933', 'support浩', '三漫陀山漫陀专卖店', '不爱打扮的姑娘', '优美善良', '佳珠旗舰店', '圆爱旗舰店', '实惠淘店30371704', '特价小商店', 'summerflowers旗舰店', '小公主滴爱', '杜主明', '玉柔工艺花坊', '甜甜百货商特卖店', '致云旗舰店'],
        sellerValues: [7497.0, 7362.0, 7253.0, 6936.0, 6618.0, 4845.0, 4739.0, 4637.0, 4634.0, 4512.0, 4242.0, 4211.0, 3765.0, 3486.0, 3413.0, 3305.0, 3041.0, 2936.0, 2914.0, 2888.0, 2884.0, 2804.0, 2719.0, 2627.0, 2591.0, 2554.0, 2522.0, 2470.0, 2453.0, 2390.0, 2332.0, 2273.0, 2239.0, 2135.0, 2130.0, 2081.0, 2069.0, 2044.0, 2041.0, 2031.0, 1970.0, 1816.0, 1797.0, 1756.0, 1716.0, 1684.0, 1683.0, 1677.0, 1661.0, 1626.0, 1620.0, 1619.0, 1596.0, 1590.0, 1586.0, 1561.0, 1549.0, 1540.0, 1508.0, 1504.0, 1479.0, 1456.0, 1443.0, 1420.0, 1385.0, 1371.0, 1358.0, 1339.0, 1333.0, 1315.0, 1312.0, 1302.0, 1287.0, 1268.0, 1250.0, 1250.0, 1229.0, 1224.0, 1205.0, 1173.0, 1165.0, 1165.0, 1153.0, 1148.0, 1112.0, 1099.0, 1091.0, 1083.0, 1069.0, 1061.0, 1061.0, 1043.0, 1036.0, 1033.0, 1024.0, 1016.0, 966.0, 963.0, 953.0, 949.0, 924.0, 920.0, 915.0, 914.0, 914.0, 902.0, 898.0, 896.0, 895.0, 883.0, 863.0, 850.0, 828.0, 819.0, 815.0, 814.0, 814.0, 814.0, 805.0, 805.0, 798.0, 794.0, 791.0, 775.0, 766.0, 759.0, 757.0, 755.0, 743.0, 738.0, 731.0, 731.0, 716.0, 713.0, 712.0, 712.0, 706.0, 701.0, 696.0, 690.0, 685.0, 684.0, 655.0, 652.0, 651.0, 648.0, 648.0, 647.0, 637.0, 636.0, 632.0, 631.0, 628.0, 621.0, 619.0, 611.0, 610.0, 610.0, 599.0, 598.0, 583.0, 583.0, 582.0, 582.0, 579.0, 568.0, 568.0, 560.0, 549.0, 536.0, 533.0, 529.0, 526.0, 518.0, 516.0, 515.0, 506.0, 504.0, 500.0, 500.0, 499.0, 495.0, 494.0, 491.0, 490.0, 488.0, 487.0, 484.0, 479.0, 476.0, 471.0, 470.0, 466.0, 466.0, 461.0, 460.0, 460.0, 456.0, 455.0, 453.0, 452.0, 445.0, 444.0, 444.0, 442.0, 436.0, 433.0, 433.0, 429.0, 429.0, 426.0, 425.0, 422.0, 420.0, 418.0, 415.0, 413.0, 413.0, 413.0, 402.0, 399.0, 398.0, 393.0, 392.0, 390.0, 389.0, 389.0, 386.0, 385.0, 383.0, 383.0, 381.0, 378.0, 376.0, 374.0, 371.0, 370.0, 369.0, 367.0, 364.0, 363.0, 362.0, 361.0, 361.0, 359.0, 358.0, 352.0, 351.0, 350.0, 350.0, 350.0, 348.0, 348.0, 348.0, 347.0, 347.0, 346.0, 345.0, 342.0, 341.0, 336.0, 331.0, 331.0, 330.0, 326.0, 320.0, 320.0, 318.0, 313.0, 313.0, 312.0, 309.0, 309.0, 307.0, 306.0, 305.0, 301.0, 301.0, 300.0, 300.0, 298.0, 296.0, 296.0, 293.0, 293.0, 292.0, 291.0, 290.0, 287.0, 285.0, 284.0, 283.0, 283.0, 282.0, 281.0, 280.0, 280.0, 279.0, 279.0, 279.0, 279.0, 279.0, 278.0, 276.0, 274.0, 271.0, 271.0, 270.0, 270.0, 266.0, 266.0, 263.0, 262.0, 261.0, 261.0, 260.0, 260.0, 260.0, 260.0, 259.0, 258.0, 257.0, 255.0, 255.0, 253.0, 252.0, 246.0, 245.0, 245.0, 243.0, 242.0, 240.0, 240.0, 240.0, 238.0, 238.0, 237.0, 235.0, 232.0, 232.0, 232.0, 232.0, 226.0, 225.0, 225.0, 224.0, 224.0, 223.0, 223.0, 222.0, 221.0, 219.0, 217.0, 214.0, 213.0, 212.0, 212.0, 210.0, 206.0, 206.0, 205.0, 205.0, 202.0, 199.0, 199.0, 199.0, 196.0, 195.0, 193.0, 193.0, 192.0, 191.0, 190.0, 190.0, 189.0, 189.0, 187.0, 186.0, 184.0, 184.0, 183.0, 183.0, 183.0, 182.0, 182.0, 182.0, 182.0, 180.0, 179.0, 178.0, 177.0, 176.0, 175.0, 174.0, 174.0, 173.0, 173.0, 172.0, 171.0, 171.0, 168.0, 168.0, 168.0, 165.0, 164.0, 163.0, 161.0, 161.0, 160.0, 160.0, 159.0, 158.0, 155.0, 155.0, 154.0, 153.0, 153.0, 152.0, 152.0, 150.0, 150.0, 149.0, 149.0, 149.0, 147.0, 147.0, 145.0, 144.0, 144.0, 144.0, 143.0, 142.0, 142.0, 141.0, 141.0, 141.0, 140.0, 139.0, 139.0, 139.0, 139.0, 139.0, 138.0, 138.0, 138.0, 138.0, 136.0, 134.0, 134.0, 132.0, 132.0, 131.0, 131.0, 130.0, 128.0, 127.0, 127.0, 126.0, 125.0, 124.0, 124.0, 123.0, 122.0, 121.0, 119.0, 119.0, 118.0, 118.0, 117.0, 117.0, 117.0, 116.0, 114.0, 112.0, 112.0, 112.0, 112.0, 111.0, 111.0, 111.0, 110.0, 110.0, 110.0, 109.0, 109.0, 107.0, 107.0, 107.0, 107.0, 106.0, 106.0, 106.0, 106.0, 105.0, 104.0, 103.0, 103.0, 103.0, 103.0, 102.0, 101.0, 101.0, 101.0, 100.0, 100.0, 99.0, 99.0, 98.0, 97.0, 97.0, 96.0, 96.0, 96.0, 96.0, 96.0, 95.0, 94.0, 94.0, 94.0, 93.0, 92.0, 92.0, 92.0, 91.0, 91.0, 91.0, 91.0, 90.0, 89.0, 88.0, 85.0, 85.0, 85.0, 84.0, 84.0, 84.0, 84.0, 83.0, 83.0, 82.0, 82.0, 81.0, 80.0, 80.0, 80.0, 80.0, 79.0, 79.0, 78.0, 78.0, 78.0, 78.0, 78.0, 78.0, 78.0, 77.0, 77.0, 77.0, 77.0, 77.0, 77.0, 76.0, 75.0, 75.0, 73.0, 73.0, 73.0, 73.0, 72.0, 72.0, 72.0, 71.0, 71.0, 71.0, 71.0, 70.0, 70.0, 70.0, 70.0, 70.0, 70.0, 69.0, 69.0, 67.0, 67.0, 67.0, 67.0, 67.0, 66.0, 66.0, 66.0, 66.0, 65.0, 65.0, 65.0, 65.0, 64.0, 64.0, 64.0, 64.0, 64.0, 64.0, 63.0, 63.0, 63.0, 62.0, 62.0, 62.0, 61.0, 61.0, 61.0, 60.0, 60.0, 59.0, 59.0, 58.0, 58.0, 58.0, 58.0, 57.0, 57.0, 57.0, 56.0, 56.0, 56.0, 55.0, 55.0, 55.0, 55.0, 55.0, 54.0, 54.0, 54.0, 54.0, 54.0, 53.0, 53.0, 53.0, 52.0, 52.0, 52.0, 52.0, 52.0, 52.0, 51.0, 51.0, 51.0, 51.0, 51.0, 50.0, 50.0, 49.0, 49.0, 49.0, 49.0, 49.0, 49.0, 48.0, 48.0, 47.0, 47.0, 47.0, 47.0, 47.0, 46.0, 45.0, 45.0, 45.0, 45.0, 45.0, 45.0, 45.0, 44.0, 44.0, 44.0, 44.0, 44.0, 43.0, 42.0, 42.0, 42.0, 42.0, 42.0, 42.0, 42.0, 42.0, 42.0, 42.0, 41.0, 41.0, 41.0, 41.0, 41.0, 41.0, 41.0, 41.0, 40.0, 40.0, 40.0, 39.0, 39.0, 39.0, 39.0, 39.0, 38.0, 38.0, 38.0, 38.0, 38.0, 37.0, 37.0, 37.0, 37.0, 37.0, 37.0, 37.0, 36.0, 36.0, 36.0, 36.0, 36.0, 36.0, 36.0, 36.0, 35.0, 35.0, 35.0, 35.0, 34.0, 34.0, 34.0, 34.0, 34.0, 34.0, 33.0, 33.0, 33.0, 33.0, 33.0, 33.0, 33.0, 33.0, 32.0, 32.0, 32.0, 32.0, 32.0, 32.0, 32.0, 32.0, 32.0, 32.0, 31.0, 31.0, 31.0, 31.0, 31.0, 31.0, 30.0, 30.0, 30.0, 30.0, 30.0, 30.0, 29.0, 29.0, 29.0, 29.0, 29.0, 29.0, 28.0, 28.0, 28.0, 28.0, 27.0, 27.0, 27.0, 27.0, 26.0, 26.0, 26.0, 26.0, 26.0, 26.0, 26.0, 26.0, 25.0, 25.0, 25.0, 25.0, 25.0, 25.0, 25.0, 25.0, 25.0, 25.0, 24.0, 24.0, 24.0, 24.0, 24.0, 24.0, 23.0, 23.0, 23.0, 23.0, 23.0, 23.0, 23.0, 22.0, 22.0, 22.0, 22.0, 22.0, 22.0, 22.0, 21.0, 21.0, 21.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 20.0, 19.0, 19.0, 19.0, 19.0, 19.0, 19.0, 19.0, 19.0, 18.0, 18.0, 18.0, 18.0, 18.0, 18.0, 18.0, 18.0, 18.0, 17.0, 17.0, 17.0, 17.0, 17.0, 17.0, 16.0, 16.0, 16.0, 16.0, 16.0, 16.0, 15.0, 15.0, 15.0, 15.0, 15.0, 15.0, 15.0, 14.0, 14.0, 14.0, 14.0, 14.0, 14.0, 14.0, 14.0, 14.0, 13.0, 13.0, 13.0, 13.0, 13.0, 13.0, 13.0, 13.0, 13.0, 13.0, 13.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 12.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 11.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 9.0, 9.0, 9.0, 9.0, 9.0, 9.0, 9.0, 9.0, 8.0, 8.0, 8.0, 8.0, 8.0, 8.0, 8.0, 8.0, 8.0, 8.0, 8.0, 7.0, 7.0, 7.0, 7.0, 7.0, 7.0, 7.0, 7.0, 7.0, 7.0, 7.0, 6.0, 6.0, 6.0, 6.0, 6.0, 6.0, 5.0, 5.0, 5.0, 5.0, 4.0, 4.0, 4.0, 4.0, 4.0, 4.0, 4.0, 4.0, 4.0, 4.0, 4.0, 4.0, 3.0, 3.0, 3.0, 3.0, 3.0, 3.0, 3.0, 3.0, 3.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 2.0, 1.0, 1.0, 1.0, 1.0, 1.0, 1.0]
      },
      currentPage: 1, // 当前显示的页数
      totalPage: 0, // 一共有多少页
      titleFontSize: 0
    }
  },
  mounted () {
    this.initChart()
    // this.getData()
    window.addEventListener('resize', this.screenAdapter)
    // 在页面加载完成的时候, 主动进行屏幕的适配
    this.screenAdapter()
  },
  destroyed () {
    // 在组件销毁的时候, 需要将监听器取消掉
    window.removeEventListener('resize', this.screenAdapter)
  },
  methods: {
    // 初始化echartInstance对象
    initChart () {
      this.chartInstance = this.$echarts.init(this.$refs.brand_bar_ref, this.theme)
      // 对图表初始化配置的控制
      const initOption = {
        title: {
          text: '▎店铺销售统计',
          left: 20,
          top: 20
        },
        grid: {
          top: '30%',
          left: '16%',
          right: '15%',
          bottom: '10%',
          containLabel: false // 距离是包含坐标轴上的文字
        },
        xAxis: {
          type: 'category',
          axisLabel: {
            interval: 0
          }
        },
        yAxis: {
          type: 'value'
        },
        tooltip: {
          trigger: 'item',
          axisPointer: {
            type: 'line',
            z: 0,
            lineStyle: {
              // color: '#2D3443'
              show: true
            }
          }
        },
        series: [
          {
            type: 'bar',
            label: {
              show: true,
              position: 'top',
              textStyle: {
                color: 'green'
              }
            },
            itemStyle: {
              // 指明颜色渐变的方向
              // 指明不同百分比之下颜色的值
              color: new this.$echarts.graphic.LinearGradient(0, 0, 1, 0, [
                // 百分之0状态之下的颜色值
                {
                  offset: 0,
                  color: '#5052EE'
                },
                // 百分之100状态之下的颜色值
                {
                  offset: 1,
                  color: '#AB6EE5'
                }
              ])
            }
          }
        ]
      }
      this.chartInstance.setOption(initOption)
      // 对图表对象进行鼠标事件的监听
      this.totalPage = Math.ceil(this.allData.sellerValues.length / 6)
      this.updateChart()
    },
    // 更新图表
    updateChart () {
      const start = (this.currentPage - 1) * 6
      const end = this.currentPage * 6
      const showNames = this.allData.sellerNames.slice(start, end)
      const showValues = this.allData.sellerValues.slice(start, end)
      const dataOption = {
        xAxis: {
          data: showNames
        },
        series: [
          {
            data: showValues
          }
        ]
      }
      this.chartInstance.setOption(dataOption)
    },
    // 当浏览器的大小发生变化的时候, 会调用的方法, 来完成屏幕的适配
    screenAdapter () {
      const titleFontSize = this.$refs.brand_bar_ref.offsetWidth / 100 * 3.6
      this.titleFontSize = titleFontSize
      // 和分辨率大小相关的配置项
      const adapterOption = {
        tooltip: {
          axisPointer: {
            lineStyle: {
              width: titleFontSize
            }
          }
        },
        series: [
          {
            barWidth: titleFontSize,
            itemStyle: {
              barBorderRadius: [titleFontSize / 2, titleFontSize / 2, 0, 0]
            }
          }
        ]
      }
      this.chartInstance.setOption(adapterOption)
      // 手动的调用图表对象的resize 才能产生效果
      this.chartInstance.resize()
    },
    toLeft () {
      this.currentPage--
      if (this.currentPage <= 0) {
        this.currentPage = this.totalPage
        this.updateChart()
      } else {
        this.updateChart()
      }
    },
    toRight () {
      this.currentPage++
      if (this.currentPage > this.totalPage) {
        this.currentPage = 1
        this.updateChart()
      } else {
        this.updateChart()
      }
    }
  },
  computed: {
    ...mapState(['theme']),
    comStyle () {
      return {
        fontSize: this.titleFontSize + 'px',
        color: getThemeValue(this.theme).titleColor
      }
    }
  },
  watch: {
    theme () {
      console.log('主题切换了')
      this.chartInstance.dispose() // 销毁当前的图表
      this.initChart() // 重新以最新的主题名称初始化图表对象
      this.screenAdapter() // 完成屏幕的适配
      this.updateChart() // 更新图表的展示
    }
  }
}
</script>

<style lang="less" scoped>

.arr-left {
  position:absolute;
  left: 3%;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  color: white;
}
.arr-right {
  position:absolute;
  right: 3%;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  color: white;
}

</style>
