<template>
  <div>
    <div class="demo_top">
      <div class="top-main">
        <el-row type="flex" class="row-bg">
          <el-col :span="6">
            <div class="grid-content bg-purple">
              <span class="span1">御览</span>
            </div>
          </el-col>
          <el-col :span="9">
            <div class="grid-content bg-purple-light">
              <div class="search">
                <el-input placeholder="请输入您要搜索的关键词" v-model="keyWord" class="input-with-select">
                  <el-button slot="append">搜一下</el-button>
                </el-input>
              </div>
            </div>
          </el-col>
          <el-col :span="9">
            <div style="margin-top: 18px;" class="grid-content bg-purple">
              <span style="margin-right: 20px;color:#d3814f;font-size: 17px;">VIP服务</span>
              <i class="el-icon-more-outline" style="margin-right: 20px;">百宝箱</i>
              <span style="margin-right: 20px;">微信公众号</span>
              <span>15939581947</span>
            </div>
          </el-col>
        </el-row>
      </div>
    </div>
    <!-- 中间部分 -->
    <div style="margin-left: 150px;margin-top: 20px;">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item><a href="/">招标公告</a></el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <div class="demo_middle">


      <!-- -->
      <div class="minddle-main">
        <el-tabs v-model="activeName" type="card" @tab-click="handleClick" stretch=true>
          <el-tab-pane label="招标公告" name="first">
            <div>
              <!-- 搜索内容 -->
              <div class="nav">
                <i-col class="title" span="2">搜索内容：</i-col>
                <i-col span="22">
                  <!-- <a href="#" v-for="(v, i) in item.items" :key="i" @click="clickrange(index, v, i)" class="text-filter">
                    <span :class="{ isActive: v.active }">{{ v.text }}</span>
                  </a> -->
                  <i-col span="22">
                    <el-radio v-for="(a,index) in Seach" :key="index" v-model="radio0" :label="a.label">{{a.name}}</el-radio>
                  </i-col>
                </i-col>
                <el-input placeholder="请输入搜索内容" v-model="searchs"></el-input>
                <el-button type="primary">搜索</el-button>
              </div>
              <!-- 选择地区 -->
              <div class="nav">
                <i-col class="title" span="2">选择地区：</i-col>
                <i-col span="22">
                  <el-checkbox-group style="display: contents;" v-model="checkedCities" @change="handleCheckedCitiesChange">
                    <el-checkbox v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
                  </el-checkbox-group>
                </i-col>
              </div>
              <!-- 行业分类 -->
              <div class="nav">
                <i-col class="title" span="2">行业分类：</i-col>
                <i-col span="22">
                  <el-radio v-for="(a,index) in Classification" :key="index" v-model="radio" :label="a.label">{{a.name}}</el-radio>
                </i-col>
              </div>
              <!-- 选择类型 -->
              <div class="nav">
                <i-col class="title" span="2">选择类型：</i-col>
                <i-col span="22">
                  <el-radio v-for="(a,index) in Type" :key="index" v-model="radio1" :label="a.label">{{a.name}}</el-radio>
                </i-col>
              </div>
              <!-- 选择金额 -->
              <div class="nav">
                <i-col class="title" span="2">选择金额：</i-col>
                <i-col span="22">
                  <el-radio v-for="(a,index) in Money" :key="index" v-model="radio2" :label="a.label">{{a.name}}</el-radio>
                </i-col>
              </div>
              <!-- 发布时间 -->
              <div class="nav">
                <i-col class="title" span="2">发布时间：</i-col>
                <i-col span="22">
                  <el-radio v-for="(a,index) in Time" :key="index" v-model="radio3" :label="a.label">{{a.name}}</el-radio>
                </i-col>
              </div>
            </div>
          </el-tab-pane>
          <el-tab-pane label="政企项目" name="second">政企项目</el-tab-pane>
          <el-tab-pane label="企业项目" name="third">企业项目</el-tab-pane>
          <el-tab-pane label="环评审批" name="fourth">环评审批</el-tab-pane>
          <el-tab-pane label="拟在建项目" name="five">拟在建项目</el-tab-pane>
          <el-tab-pane label="历史数据" name="six">历史数据</el-tab-pane>
          <el-tab-pane label="大型项目" name="seven">大型项目</el-tab-pane>
          <el-tab-pane label="直接采购" name="eight">直接采购</el-tab-pane>
          <el-tab-pane label="业主追踪" name="nine">业主追踪</el-tab-pane>
        </el-tabs>
      </div>
      <!--  -->

    </div>
    <div class="main-below">
      <el-row :gutter="20">
        <el-col :span="16">
          <div class="grid-content bg-purple">

            <div class="left">
              <div style="height: 50px;margin-top: 10px;margin-left: 20px;">
                <el-col :span="19">
                  <div style="margin-top: 10px;" class="grid-content bg-purple">
                    共找到<span style="color: red;">{{msg}}</span>条招标公告信息
                  </div>
                </el-col>
                <el-col :span="5">
                  <div class="grid-content bg-purple">
                    <el-button class="button1" icon="el-icon-view">立即订阅</el-button>
                  </div>
                </el-col>
              </div>
              <div style="height: 40px;background-color: #f0f7ff;text-align: center;">
                <span style="line-height: 40px;">订阅成功后，将通过微信、短信、邮件为您推送最新招投标动态，</span>
                <el-link :underline="false" style="color: #80c3fa;">立即设置></el-link>
              </div>
              <!--  -->
              <div class="dynamic" :data="XinXi.slice((currentPage3-1)*pageSize,currentPage3*pageSize)" v-for="(c,index) in XinXi"
                :key="index">
                <div class="p1">
                  <span class="span2">招标</span>
                </div>
                <span style="line-height: 30px;">{{c.name}}</span>
                <el-col :span="4">
                  <div class="grid-content bg-purple">
                    <div class="p2">
                      {{c.t1}}
                    </div>
                  </div>
                </el-col>
                <el-col :span="13">
                  <div class="grid-content bg-purple-light">
                    <div class="p3">{{c.t2}}</div>
                  </div>
                </el-col>
                <el-col :span="7">
                  <div class="grid-content bg-purple">

                    <label style="float: right;color: #a6a6a6;margin-top: 20px;">{{c.times}}</label>
                  </div>
                </el-col>
              </div>
              <!-- 分页开始 -->
              <div class="block">
                <el-pagination background @size-change="handleSizeChange" @current-change="handleCurrentChange"
                  :current-page.sync="currentPage3" :page-size="pageSize" layout="prev, pager, next, jumper" :total="total">
                </el-pagination>
              </div>
              <!-- 分页结束 -->
            </div>

          </div>
        </el-col>
        <el-col :span="8">

          <div class="grid-content bg-purple">
            <div class="right">
              <div class="hot">
                招标搜索热词
              </div>
              <div style="margin-top: 10px;margin-left: 20px;border-bottom: 1px solid #ededed;">
                <a style="margin-right: 30px;color: #3a3a3a;" href="#" v-for="(item,index) in searchCi" :key="index">{{item.name}}</a>
              </div>

              <div class="haha">

              </div>

              <div class="xia">
                <div style="height: 40px;margin-top: 10px;margin-left: 20px;border-bottom: 1px solid #ededed;">
                  热门招标信息
                </div>
                <div v-for="(b,index) in searchXi" :key="index" style="height: 60px;margin-top: 10px;margin-left: 20px;border-bottom: 1px solid #ededed;">
                  <a style="margin-right: 30px;color: #000000;" href="#">{{b.name}}</a></br>
                  <label style="color: #9a9a9a;">{{b.time}}</label>
                </div>
              </div>
              <div class="haha">

              </div>
              <div class="xia">
                <div style="height: 40px;margin-top: 10px;margin-left: 20px;border-bottom: 1px solid #ededed;">
                  政府采购信息
                </div>
                <div v-for="(b,index) in searchXin" :key="index" style="height: 60px;margin-top: 10px;margin-left: 20px;border-bottom: 1px solid #ededed;">
                  <a style="margin-right: 30px;color: #000000;line-height: 30px;" href="#">{{b.name}}</a></br>
                  <label style="color: #c8c8c8;">{{b.time}}</label>
                </div>
              </div>
            </div>

          </div>
        </el-col>
      </el-row>
    </div>


    <div class="dome_below">
      <div class="below-nav">
        <el-row :gutter="20">
          <el-col :span="4">
            <div class="grid-content bg-purple">
              <div class="h2">
                <span>御览</span>
              </div>
            </div>
          </el-col>
          <el-col :span="16">
            <div class="grid-content bg-purple">
              <div class="h1">
                <span>一站式招标信息发布与精准查询平台</span><br />
                <a href="">关于我们</a>
                <a href="">联系我们</a>
                <a href="">会员服务</a>
                <a href="">付款方式</a>
                <a href="">招标法规</a>
                <a href="">网站声明</a>
                <a href="">友情链接</a><br />
                <a href="">版权所有2008-2020沪</a>
                <a href="">御览招标信息科技有限公司</a>
                <a href="">ICP备2020025609号</a>
              </div>
            </div>
          </el-col>
          <el-col :span="4">
            <div class="grid-content bg-purple"></div>
          </el-col>
        </el-row>
      </div>
    </div>

  </div>
</template>

<script>
  const cityOptions = ['全国', '北京', '上海', '天津', '重庆', '黑龙江', '吉林', '辽宁', '内蒙古', '河北', '山西'];
  export default {

    data() {
      return {
        // 分页

        currentPage3: 1,
        pageSize: 5,
        total: 7,
        msg: "10000+",
        keyWord: "",
        searchs: "",
        activeName: 'first',
        radio0: '1',
        Seach: [{
            label: "1",
            name: "全部",
          },
          {
            label: "2",
            name: "标题",
          },
          {
            label: "3",
            name: "内容",
          },
        ],
        radio: '1',
        Classification: [{
            label: "1",
            name: "全部",
          },
          {
            label: "2",
            name: "工程建筑",
          },
          {
            label: "3",
            name: "政府部门",
          },
          {
            label: "4",
            name: "交通运输",
          },
          {
            label: "5",
            name: "环保绿化",
          },
          {
            label: "6",
            name: "医疗卫生",
          },
          {
            label: "7",
            name: "仪器仪表",
          },
          {
            label: "8",
            name: "水利水电",
          },
          {
            label: "9",
            name: "能源化工",
          },
        ],
        // 选择类型
        radio1: '5',
        Type: [{
            label: "1",
            name: "全部",
          },
          {
            label: "2",
            name: "采购公示",
          },
          {
            label: "3",
            name: "拟在建项目",
          },
          {
            label: "4",
            name: "出让公告",
          },
          {
            label: "5",
            name: "招标公告",
          },
          {
            label: "6",
            name: "变更答疑",
          },
          {
            label: "7",
            name: "评标公告",
          },
          {
            label: "8",
            name: "中标公告",
          },
          {
            label: "9",
            name: "招标公告",
          },
        ],
        // 选择金额
        radio2: '4',
        Money: [{
            label: "1",
            name: "全部",
          },
          {
            label: "2",
            name: "1000-5万",
          },
          {
            label: "3",
            name: "5-20万",
          },
          {
            label: "4",
            name: "50-100万",
          },
          {
            label: "5",
            name: "100-500万",
          },
          {
            label: "6",
            name: "500-1000万",
          },
          {
            label: "7",
            name: "1000万以上",
          },
        ],
        // 发布时间
        radio3: '1',
        Time: [{
            label: "1",
            name: "全部",
          },
          {
            label: "2",
            name: "一个月内",
          },
          {
            label: "3",
            name: "3个月内",
          },
          {
            label: "4",
            name: "6个月内",
          },
          {
            label: "5",
            name: "一年内",
          },
          {
            label: "6",
            name: "不限",
          },
        ],


        // 信息
        XinXi: [{
            name: "茂名市茂南区自然资源局茂名市茂南区自然资源局复印机粉盒/墨粉网上商城合同采购合同",
            t1: "广东",
            t2: "2021,04万",
            times: "2020-02-28 13:23:54"
          },
          {
            name: "茂名市茂南区自然资源局茂名市茂南区自然资源局复印机粉盒/墨粉网上商城合同采购合同",
            t1: "广东",
            t2: "2021,04万",
            times: "2020-02-28 13:23:54"
          },
          {
            name: "茂名市茂南区自然资源局茂名市茂南区自然资源局复印机粉盒/墨粉网上商城合同采购合同",
            t1: "广东",
            t2: "2021,04万",
            times: "2020-02-28 13:23:54"
          }, {
            name: "茂名市茂南区自然资源局茂名市茂南区自然资源局复印机粉盒/墨粉网上商城合同采购合同",
            t1: "广东",
            t2: "2021,04万",
            times: "2020-02-28 13:23:54"
          },
          {
            name: "茂名市茂南区自然资源局茂名市茂南区自然资源局复印机粉盒/墨粉网上商城合同采购合同",
            t1: "广东",
            t2: "2021,04万",
            times: "2020-02-28 13:23:54"
          },
          {
            name: "茂名市茂南区自然资源局茂名市茂南区自然资源局复印机粉盒/墨粉网上商城合同采购合同",
            t1: "广东",
            t2: "2021,04万",
            times: "2020-02-28 13:23:54"
          },
          {
            name: "茂名市茂南区自然资源局茂名市茂南区自然资源局复印机粉盒/墨粉网上商城合同采购合同",
            t1: "广东",
            t2: "2021,04万",
            times: "2020-02-28 13:23:54"
          },
          {
            name: "茂名市茂南区自然资源局茂名市茂南区自然资源局复印机粉盒/墨粉网上商城合同采购合同",
            t1: "广东",
            t2: "2021,04万",
            times: "2020-02-28 13:23:54"
          },
        ],


        // 招标搜索热词
        searchCi: [{
            name: "建筑",
          },
          {
            name: "绿化",
          },
          {
            name: "物业",
          },
          {
            name: "广告",
          },
          {
            name: "大数据",
          },
          {
            name: "消防",
          },
          {
            name: "软件",
          },
          {
            name: "服饰",
          },
          {
            name: "能源",
          },
          {
            name: "银行",
          },
          {
            name: "工程",
          },
        ],



        // 热门招标信息
        searchXi: [{
            time: "2020-02-28",
            name: "广东民间工艺博物馆安全技术防范...",
          },
          {
            time: "2020-02-28",
            name: "广东民间工艺博物馆安全技术防范...",
          },
          {
            time: "2020-02-28",
            name: "广东民间工艺博物馆安全技术防范...",
          },
          {
            time: "2020-02-28",
            name: "广东民间工艺博物馆安全技术防范...",
          },
          {
            time: "2020-02-28",
            name: "广东民间工艺博物馆安全技术防范...",
          },


        ],

        // 政府采购信息
        searchXin: [{
            time: "2020-02-28",
            name: "龙口市2019年农村公测货物采购安装...",
          },
          {
            time: "2020-02-28",
            name: "广东民间工艺博物馆安全技术防范...",
          },
          {
            time: "2020-02-28",
            name: "龙口市2019年农村公测货物采购安装...",
          },
          {
            time: "2020-02-28",
            name: "广东民间工艺博物馆安全技术防范...",
          },
          {
            time: "2020-02-28",
            name: "龙口市2019年农村公测货物采购安装...",
          },


        ],
        checkAll: false,
        checkedCities: ['全国'],
        cities: cityOptions,
        isIndeterminate: true
      };
    },
    methods: {
      handleClick(tab, event) {
        console.log(tab, event);
      },
      //
      handleCheckedCitiesChange(value) {
        let checkedCount = value.length;
        this.checkAll = checkedCount === this.cities.length;
        this.isIndeterminate = checkedCount > 0 && checkedCount < this.cities.length;
      },
      // 分页
      handleSizeChange(val) {
        this.pageSize = val;
        console.log(`每页 ${val} 条`);
      },
      handleCurrentChange(val) {
        this.currentPage3 = val;
        console.log(`当前页: ${val}`);
      }
    }
  }
</script>
<style scoped="scoped">
  /deep/ .el-radio__inner {
    display: none;
  }

  .demo_top {
    width: 100%;
    height: 60px;
    background-color: #FFFFFF;
    /* border: 1px solid black; */
  }

  .top-main {
    width: 80%;
    height: 55px;
    /* border: 1px solid red; */
    margin: 0 auto;
  }

  .span1 {
    font-size: 35px;
    color: cadetblue;
  }

  .search {
    margin-top: 10px;
  }

  .search el-button {
    background-color: blue;
  }

  .input-with-select {
    width: 320px;
  }

  .el-input__inner {
    height: 30px;
  }

  /* 中间部分 */
  .demo_middle {
    width: 80%;
    /* border: 1px solid red; */
    background-color: #FFFFFF;
    margin: 0 auto;
  }

  .minddle-main {
    margin-top: 20px;
    line-height: 70px;
  }

  .text-filter {
    display: inline-block;
    color: black;
    width: 60px;
  }

  .minddle-main .el-input {
    width: 200px;
  }

  .nav .el-button,
  .el-input {
    border-radius: 0px;
  }

  .nav {
    /* margin-top: 40px; */
    margin-left: 40px;
  }

  .title {
    color: grey;
    height: 40px;
  }

  a {
    text-decoration: none;

  }

  .hot {
    height: 40px;
    line-height: 40px;
    margin-top: 10px;
    margin-left: 20px;
    border-bottom: 1px solid #ededed;
    line-height: 32px;
    margin-bottom: 30px;
  }

  /* 中下部分 */
  .main-below {
    width: 80%;
    /* border: 1px solid red; */
    margin: 0 auto;
    margin-top: 30px;
  }

  .left {
    height: 300px;
    /* border: 1px solid black; */
    background-color: #FFFFFF;
    /* margin-top: 10px; */
    /* margin-left: 20px; */
  }

  .button1 {
    margin-top: 5px;
    height: 34px;
    background-color: white;
  }

  .dynamic {
    height: 110px;
    background-color: #FFFFFF;
    border-bottom: 1px solid #eeeeee;
    /* border: 1px solid black; */
  }

  .dynamic span:hover {
    color: blue;
    cursor: pointer;
  }

  .p1 {
    display: inline-block;
    width: 40px;
    height: 20px;
    margin-left: 10px;
    border-radius: 3px;
    background-color: #01b061;
  }

  .p2 {
    width: 40px;
    height: 20px;
    border-radius: 3px;
    margin-top: 20px;
    background-color: #f0f7ff;

    font-size: 12px;
    padding-left: 10px;
    color: #2681ea;
  }

  .p3 {
    width: 90px;
    height: 20px;
    margin-top: 20px;
    border-radius: 3px;
    background-color: #fff1e8;

    font-size: 12px;
    padding-left: 10px;
    color: #e88154;
  }

  .span2 {
    text-align: center;
    font-size: 12px;
    margin-left: 5px;
    color: #FFFFFF;
  }

  .block {
    margin-top: 10px;
    text-align: center;
  }

  .right {
    background-color: #FFFFFF;
    /* border: 1px solid #0000FF; */
  }

  .haha {
    height: 20px;
    background-color: #f6f6f6;
  }

  .xia {
    margin-top: 20px;
  }

  .dome_below {
    width: 100%;
    height: 150px;
    position: relative;
    top: 70px;
    background-color: #22273b;
  }

  .below-nav {
    margin: 0 auto;
    /* border: 1px solid red; */
    height: 120px;
    width: 80%;
  }

  .h2 {
    margin-top: 40px;
  }

  .h2 span {
    color: #FFFFFF;
    font-size: 60px;
  }

  .h1 {
    margin-top: 40px;
  }

  .h1 span {
    font-size: 20px;
    color: #FFFFFF;
    line-height: 40px;
  }

  .h1 a {
    line-height: 20px;
    font-size: 13px;
    color: #FFFFFF;
  }
</style>
