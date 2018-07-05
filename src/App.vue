<template>
  <div id="app">
    <div id="content">
      <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
      <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
    <div id="foot">
      <ThankEditor ref="thankEditor" :markdown="currentThankMarkdown" :enableHtml="enableHtml"></ThankEditor>
    </div>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import ThankEditor from './components/ThankEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor,
      ThankEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Inspired by http://strml.net/
* 源码地址 https://github.com/yuxd/anires
* 各位领导，大家好，我是余小东。
* 今天我有幸来竞聘主任助理！
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .1s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222); background: rgb(0,64,64);
}
#content{
  height:70vh;
  margin:0;
}
#foot{
  height:29vh;
  margin:0;
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 50vw; height: 70vh;
  background: rgb(20,20,20);
}
/* 代码高亮 */
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 50vw; height: 70vh;
  border: 1px solid;
  background: rgb(200,200,200); color: #222;
  overflow: auto;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(-10deg) translateZ(-100px) ;
          transform: rotateY(-10deg) translateZ(-100px) ;
}
/* 开始写简历 */
`, `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`, `/* 写封感谢信。
 * 感谢大家对我的关注。
 */
.styleEditor{
    width:50vw;height:70vh;
}

.resumeEditor{
   width:50vw;height:70vh;
}

.thankEditor{
  position: relative; left: 0; top: 0;
  background: #E9D9BB;
  color: #001C42;
  overflow: auto;
}

.thankEditor {
  width: 99vw; height: 45vh;
  border: 1px solid #ccc;
  font-size: .9em;
}
`,`
.thankEditor{
  padding: .5em;  margin: .5em; margin-top:1em;
}

.thankEditor ul,.thankEditor ol{
  list-style: none;
}
.thankEditor ul> li::before{
  content: '☞'; color: red;
  margin-right: .5em;
}
.thankEditor ol {
  counter-reset: section;
}
.thankEditor ol li::before {
  counter-increment: section;
  content: counters(section, "☞") " ";
  margin-right: .5em;
}

.thankEditor{
  width: 99vw; height: 45vh;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateX(-10deg) translateZ(-200px);
          transform: rotateX(-10deg) translateZ(-200px);
}

`],
        currentMarkdown: '',
        currentThankMarkdown: '',
        fullMarkdown: `

个人简介
====

- 1982年5月8日出生于湖南省平江县木金乡下江村。
- 年少时父辈以方先知（原湖南省国土资源厅厅长,现湖南省财经委员会主任委员）等同村优秀人物激励，以之为榜样努力好学。
- 自小学六年级开始多次任学生会主席，班干部等至高中毕业在中学社团活动中表现活跃，然此经历淡了从政为官的心。
- 父亲为退伍军人，长途货运司机，小时候常跟随外出历经诸多不平之事，立志成为一名律师或人民警察但都未能遂愿。
- 2006年衡阳师院完成大学学业时年已24岁，拜天岳出汩水顺江而下至华亭，在上海辗转4年，2009年适遇车祸所幸无碍，思念故土亲人于2010年回长沙。
- 2010年结婚2011年育得一子取名余凡。
- 现为金杯电工总部信息中心软件工程师。
工作经历
====
- 2016年07月至2018年07月   总部信息中心/优卡运营管理部	任开发工程师/信息技术主管负责优卡信息化建设
- 2016年02月至2016年07月   湖南希尚网络科技有限公司任架构师负责线上分销平台高性能架构优化
- 2013年03月至2016年02月	 北京通联智慧旅投有限公司/湖南三英特旅游智能技术有限公司任研发中心总监
分管智慧旅游技术研发与数据中心运维
- 2012年03月至2013年03月	 湖南创发科技有限责任公司任高级软件工程师 负责电信189网厅开发、南京代销商业务平台开发
- 2010年03月至2012年03月	 湖南拓维信息系统股份有限公司任高级软件工程师先后负责移动业务呼叫中心开发、农信通项目管理、
校讯通开发、手机统一开放平台研发
- 2006年05月至2010年03月  上海九闻信息技术有限公司	工程师/项目经理先后负责巨人集团（征途网络科技）呼叫中心集成开发、
上海银行呼叫中心集成开发、南京电力预警系统架构、东方航空故障报修系统、法国雅高集团呼叫中心项目经理

竞聘优势
====
- 具备金杯电工信息化条线研发和团队管理经验
- 一家思科全国一级代理商企业、两家湖南省一级集成资质企业，一家长沙市高新技术认定企业工作经验。
- 丰富的软件研发技术工作经验
- 丰富的项目管理、技术管理经验，从０到有团队管理经验
- 较前瞻的IT治理思想

岗位认识
====
- 责任重大，多项重要工作包括项目统筹、团队管理、政策工作 带“协助”和“全责”标记
- 工作关系复杂，有内部客户、外部客户、供应商、政府关系处理
- 工作技能要求全面
- 总的关注信息化投资效益，科学处理关系

工作设想
====
- 积极建言提方案、务实执行信息化战略
- 管理方式学标杆，公司财务体系多年优秀部门，有章可依
- 工作输出服务化，效益绩效客观数据呈现，成本部门变创收部门
- IT治理标准化，外包流程、供应商及设备引入、研发流程、运维流程、事业部协作流程
- 节俭降本、创新开源
`, thanksMarkdown: `
鸣谢
----

* 感谢廖占洲代表的人力资源部让我有机会加入金杯电工大家庭。
* 感谢廖国峰代表的公司领导授予2016年优秀新员工称号。
* 感谢伏广旭代表的能翔优卡经营层提供共享汽车服务平台、充电桩服务平台、长短租管理平台项目历炼机会。
* 感谢优卡及信息中心开发、运维组同事同心协助、感谢优卡事业部授予2017年优秀管理者。
* 感谢周总代表的公司领导授予2017年劳动模范。
* 感谢黄总代表公司同事在我困境和低谷时伸出援助之手，感受大家庭的温暖。
* 感谢自己努力工作争取公司同事的认同、时刻准备拥抱公司变化。
* 感谢各位领导同事的聆听。

  `
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0);
        await this.progressivelyShowResume();
        await this.progressivelyShowStyle(1);
        await this.showHtml();
        await this.progressivelyShowStyle(2);
        await this.progressivelyShowThanks();
        await this.progressivelyShowStyle(3)
      },
      showHtml() {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) {
              return
            }
            // 计算前 n 个 style 的字符总数
            let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
            let prefixLength = length - style.length
            if (this.currentStyle.length < length) {
              let l = this.currentStyle.length - prefixLength
              let char = style.substring(l, l + 1) || ' '
              this.currentStyle += char
              if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                this.$nextTick(() => {
                  this.$refs.styleEditor.goBottom()
                })
              }
              setTimeout(showStyle, interval)
            } else {
              resolve()
            }
          }).bind(this)
          showStyle()
        })
      },
      progressivelyShowResume() {
        return new Promise((resolve, reject) => {
          let length = this.fullMarkdown.length
          let interval = this.interval
          let showResume = () => {
            if (this.currentMarkdown.length < length) {
              this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
              let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
              let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.resumeEditor) {
                this.$nextTick(() => this.$refs.resumeEditor.goBottom())
              }
              setTimeout(showResume, interval)
            } else {
              resolve()
            }
          }
          showResume()
        })
      },
      progressivelyShowThanks() {
        return new Promise((resolve, reject) => {
          let length = this.thanksMarkdown.length
          let interval = this.interval
          let showThanks = () => {
            if (this.currentThankMarkdown.length < length) {
              this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
              let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
              let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.thankEditor) {
                this.$nextTick(() => this.$refs.thankEditor.goBottom())
              }
              setTimeout(showThanks, interval)
            } else {
              resolve()
            }
          }
          showThanks()
        })
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  html {
    min-height: 100vh;
  }

  * {
    box-sizing: border-box;
  }
</style>
