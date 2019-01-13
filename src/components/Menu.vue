<template>
	<div class="menu">
		<dl>
			<dt>全部分类</dt>
			<dd v-for="(item,index) in menu"
					:key="index"
					@mouseenter="mouseEnter"
					@mouseleave="mouseLeave">
				<i :class="item.type"></i>
				{{item.name}}
				<span class="arrow"></span>
			</dd>
		</dl>
		<div class="detail-wrapper"
				 v-if="currentType"
				 @mouseenter="detailMouseEnter"
				 @mouseleave="detailMouseLeave">
			<div class="detail" v-for="(item, index) in currentCategory.detail" :key="index">
				<div class="detail-title">
					<h2>{{item.title}}</h2>
					<a href="#">更多<i class="detail-arrow-right"></i></a>
				</div>
				<div class="detail-content">
					<a href="#" v-for="(item, index) in item.content" :key="index">{{item}}</a>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
/* eslint-disable */
	export default {
		data () {
			return {
				currentType: '',
				menu: [
					{
						name: '美食',
						type: 'food',
						detail: [
							{
								title: '美食',
								content: [
									'代金券',　'甜点',　'饮品',　'火锅',　'自助餐',　'小吃',　'快餐',　'日韩料理',　'西餐',　'聚餐宴请',　'烧烤烤肉',　'东北菜',　'川湘菜',　'江浙菜',　'香锅烤鱼',　'粤港菜',　'中式烧烤',　'烤串',　'西北菜',　'咖啡',　'酒吧',　'茶馆',　'云贵菜',　'东南亚菜',　'海鲜素食',　'台湾/客家菜',　'创意菜',　'汤/粥/炖菜',　'蒙餐新疆菜',　'其他美食',　'京菜鲁菜'
								]
							}
						]
					},
					{
						name: '外卖',
						type: 'takeout',
						detail: [
							{
								title: '外卖',
								content: [
									'美团外卖'
								]
							}
						]
					},
					{
						name: '酒店',
						type: 'hotel',
						detail: [
							{
								title: '酒店星级',
								content: [
									'经济型舒适', '三星高档', '四星豪华', '五星'
								]
							}
						]
					},
					{
						name: '榛果民宿',
						type: 'homestay',
						detail: [
							{
								title: '热门城市',
								content: [
									'上海', '成都', '北京', '重庆', '南京', '杭州', '广州', '西安', '大连'
								]
							}
						]
					},
					{
						name: '猫眼电影',
						type: 'movie',
						detail: [
							{
								title: '热映电影',
								content: [
									'大黄蜂', '“大”人物', '白蛇：缘起', '来电狂响', '命运之夜——天之杯：恶兆之花', '飞驰人生', '新喜剧之王', '疯狂的外星人', '海王', '养家之人'
								]
							},
							{
								title: '热门影院',
								content: [
									'耀莱成龙国际影城', '大地影院', '保利国际影城', '万达影城', '博纳国际影城', '飞驰人生', 'CGV影城', '橙天嘉禾影城', '金逸影城', '中影国际影城', '新华国际影城'
								]
							}
						]
					},
					{
						name: '机票 / 火车票',
						type: 'airport',
						detail: [
							{
								title: '机票',
								content: [
									'国内机票', '国内机票'
								]
							},
							{
								title: '火车票',
								content: [
									'火车票'
								]
							}
						]
					},
					{
						name: '休闲娱乐 / KTV',
						type: 'ktv',
						detail: [
							{
								title: '休闲娱乐',
								content: [
									'足疗按摩', '洗浴/汗蒸', '酒吧', '密室逃脱', '轰趴馆', '茶馆', '私人影院', 'DIY手工坊', '采摘/农家乐', '网吧网咖', '游乐游艺', 'VR', '桌面游戏', '真人CS', '棋牌室', '其他玩乐'
								]
							},
							{
								title: 'KTV',
								content: [
									'KTV'
								]
							}
						]
					},
					{
						name: '生活服务',
						type: 'life',
						detail: [
							{
								title: '生活服务',
								content: [
									'衣物/皮具洗护', '家政', '搬家运输', '送水', '充值缴费', '服饰/鞋包养护', '开锁换锁', '居家维修', '管道疏通', '家电维修清洗', '电脑维修', '手机维修', '证件照/肖像摄影', '照片冲印/图文文印', '商务服务/法律服务', '文化传媒机构', '成人用品/情趣用品'
								]
							}
						]
					},
					{
						name: '丽人 / 美发 / 医学美容',
						type: 'hair',
						detail: [
							{
								title: '丽人',
								content: [
									'美发', '美甲', '美睫', '美容', '美体', '医学美容', '瑜伽', '舞蹈', '瘦身纤体', '韩式定妆', '祛痘', '纹身', '化妆品'
								]
							}
						]
					},
					{
						name: '结婚 / 婚纱摄影 / 婚宴',
						type: 'marry',
						detail: [
							{
								title: '结婚',
								content: [
									'婚纱摄影', '旅拍', '个性写真', '婚宴', '婚庆公司', '婚纱礼服', '西服定制', '婚戒', '首饰', '婚车租赁', '司仪主持', '彩妆造型', '婚礼跟拍', '婚礼', '小礼品', '更多婚礼服务'
								]
							}
						]
					},
					{
						name: '亲子 / 儿童乐园 / 幼教',
						type: 'offspring',
						detail: [
							{
								title: '儿童乐园',
								content: [
									'婴儿游泳', '其它亲子游乐'
								]
							},
							{
								title: '幼儿教育',
								content: [
									'早教中心', '少儿英语', '智力开发', '托班/幼儿园', '幼儿教育', '其他幼儿教育'
								]
							},
							{
								title: '亲子摄影',
								content: [
									'儿童摄影', ' 孕妇写真', '上门拍', '其他亲子摄影'
								]
							},
							{
								title: '孕产护理',
								content: [
									'月子会所', ' 产后恢复', '妇幼医院', '孕产用品', '开奶催乳', '月嫂', '亲子购物', '宝宝派对', '亲子服务'
								]
							}
						]
					},
					{
						name: '运动健身 / 健身中心',
						type: 'sport',
						detail: [
							{
								title: '运动健身',
								content: [
									'健身中心', '武术场馆', '游泳馆', '羽毛球馆', '溜冰场', '射箭馆', '篮球场', '网球馆', '台球馆', '乒乓球足球场', '高尔夫场', '保龄球馆', '体育场馆', '马术场', '壁球馆', '更多运动'
								]
							}
						]
					},
					{
						name: '家装 / 建材 / 家居',
						type: 'furniture',
						detail: [
							{
								title: '装修设计',
								content: [
									'半包装修', '全包装修', '清包装修'
								]
							},
							{
								title: '装修建材',
								content: [
									'地板瓷砖', '石材', '橱柜', '灯饰照明', '厨卫洁具', '油漆涂料', '集成吊顶', '墙纸墙艺', '门窗', '木材板材', '家用五金', '电工电料', '楼梯管材管件'
								]
							},
							{
								title: '家具家居',
								content: [
									'家具', '床上用品/家纺', '家居饰品', '厨具餐具', '智能家居'
								]
							},
							{
								title: '家装卖场',
								content: [
									'建材卖场', '家居卖场', '灯饰卖场'
								]
							}
						]
					},
					{
						name: '学习培训 / 音乐培训',
						type: 'study',
						detail: [
							{
								title: '音乐培训',
								content: [
									'钢琴', '吉他', '小提琴', '古筝', '架子鼓', '声乐', '其他音乐培训'
								]
							},
							{
								title: '职业技术',
								content: [
									'美容', '化妆', '会计', 'IT', '厨艺', '管理培训', '摄影培训', '司法考试', '公务员培训', '其他职业培训'
								]
							},
							{
								title: '外语培训',
								content: [
									'英语', '日语', '韩语', '法语', '德语', '汉语', '俄语', '西班牙语', '其他外语'
								]
							},
							{
								title: '美术培训',
								content: [
									'绘画', '书法', '其他美术' 
								]
							}
						]
					},
					{
						name: '医疗健康 / 宠物 / 爱车',
						type: 'health',
						detail: [
							{
								title: '医疗健康',
								content: [
									'医院', '齿科', '口腔', '体检中心', '药店', '中医', '其他健康服务'
								]
							},
							{
								title: '爱车',
								content: [
									'洗车', '租车', '加油站', '维修保养', '驾校', '汽车美容', '陪练', '汽车用品', '停车场', '汽车保险', '4S店/汽车销售', '更多汽车服务', '机油保养', '汽车报价', '二手车', '广告驾校', '交警队', '汽车改装', '汽车配件'
								]
							},
							{
								title: '宠物',
								content: [
									'宠物店', '宠物医院'
								]
							}
						]
					},
					{
						name: '酒吧 / 密室逃脱',
						type: 'bar',
						detail: [
							{
								title: '玩乐',
								content: [
									'KTV', '酒吧', '密室逃脱', '游乐游艺', '网吧网咖', '私人影院', 'DIY手工坊', '桌面游戏', '采摘/农家乐', '棋牌室', '轰趴馆', '真人CS', 'VR', '其他玩乐'
								]
							}
						]
					}
				]
			}
		},
		computed: {
			// 根据currentType值获取对应的菜单详情数据
			currentCategory() {
				return this.menu.filter(item =>	this.currentType === item.type)[0]
			}
		},
		methods: {
			mouseEnter(e) {
				// 获取鼠标移入的dd节点的i子节点属性名
				clearTimeout(this.timer)
				this.currentType = e.target.childNodes[0].className
			},
			mouseLeave() {
				this.timer =  setTimeout(() => {
					this.currentType = ''
				})
			},
			detailMouseEnter() {
				clearTimeout(this.timer)
			},
			detailMouseLeave() {
				this.currentType = ''
			}
		}
	}
</script>

<style lang="stylus" scoped>
	@import "~assets/stylus/index.styl"
	
	.menu
		margin-left: 100px
		margin-top: 100px
		width: 230px
		height: 475px
		color: #fff
		background: linear-gradient(-180deg, rgba(2, 181, 157, .85) 2%, rgba(22, 146, 183, .85) 100%)
		dl
			dt
				padding-top: 15px
				padding-left: 15px
				box-sizing: border-box
				height: 50px
				font-size: 16px
			dd
				position: relative
				padding: 2px 12px
				box-sizing: border-box
				height: 26px
				font-size: 14px
				cursor: pointer
				&:hover
					background: rgba(255, 255, 255, .2)
					i
						opacity: 1
				i
					margin-right: 11px
					font-family: 'meituan'
					font-size: 14px
					font-style: normal
					opacity: 0.3
					&:before
						display: inline-block
						width: 14px
						height: 14px
				.food
					&:before
						content: '\e622'
				.takeout
					&:before
						content: '\e630'
				.hotel
					&:before
						content: '\e62a'
				.homestay
					&:before
						content: '\e631'
				.movie
					&:before
						content: '\e62c'
				.airport
					&:before
						content: '\e632'
				.ktv
					&:before
						content: '\e627'
				.life
					&:before
						content: '\e633'
				.hair
					&:before
						content: '\e626'
						transform: scale(0.7)
				.marry
					&:before
						content: '\e629'
				.offspring
					&:before
						content: '\e623'
				.sport
					&:before
						content: '\e62b'
				.furniture
					&:before
						content: '\e625'
				.study
					&:before
						content: '\e624'
				.health
					&:before
						content: '\e628'
				.bar
					&:before
						content: '\e621'
				.arrow
					position: absolute
					top: 11px
					right: 15px
					display: block
					width: 4px
					height: 4px
					border-top: 1px solid #fff
					border-right: 1px solid #fff
					transform: rotate(45deg)
		.detail-wrapper
			position: absolute
			box-sizing: border-box
			left: 330px
			top: 159px
			z-index: 999
			width: 400px
			height: 416px
			background: #fff
			.detail
				padding: 0 30px 12px
				color: #ccc
				overflow: hidden
				.detail-title
					padding: 20px 0 2px
					height: 22px
					line-height: 22px
					border-bottom: 1px solid #e5e5e5
					h2
						float: left
						font-size: 16px
						font-weight: 400
						color: #222
					a
						position: relative
						float: right
						margin-right: 12px
						font-size: 12px
						color: #999
					.detail-arrow-right
						position: absolute
						right: -8px
						top: 8px
						display: block
						width: 4px
						height: 4px
						border-top: 1px solid #999
						border-right: 1px solid #999
						transform: rotate(45deg)
				.detail-content
					a
						float: left
						margin: 10px 16px 0 0
						font-size: 12px
						color: #999
						&:hover
							color: #41B883
</style>