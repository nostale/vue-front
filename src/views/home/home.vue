<template>
<div>
  <div class="headbar">
    <Collapse v-model="value" style="min-width:1200px;">
      <Panel name="1">
        选项卡
        <div class="" slot="content" style="margin-left:10px;padding-top:5px;padding-bottom:5px;">
          <div class="">
            <span style="padding-right:20px;padding-top:10px;">平台渠道 ：</span>
            <Tag checkable color="blue">全部</Tag>
            <Tag checkable :checked="false" color="blue">标签一</Tag>
            <Tag checkable :checked="false" color="blue">标签二</Tag>
            <Tag checkable :checked="false" color="blue">标签三</Tag>
            <Tag checkable :checked="false" color="blue">标签四</Tag>
            <span class="" style="float:right">
              <ButtonGroup>
                <Button type="primary" size="small">
                  筛选
                </Button>
                <Button size="small">
                  搜索
                </Button>
              </ButtonGroup>
            </span>
          </div>
          <div class="" style="margin-top:5px;">
            <span style="padding-right:20px;">店铺账号 ：</span>
            <Tag checkable color="blue">全部</Tag>
            <Tag checkable :checked="false" color="blue">标签一</Tag>
            <Tag checkable :checked="false" color="blue">标签二</Tag>
            <Tag checkable :checked="false" color="blue">标签三</Tag>
            <Tag checkable :checked="false" color="blue">标签四</Tag>
          </div>
        </div>
        <div class="" slot="content" style="padding-left:10px;border-top:1px #e9eaec solid;padding-top:5px;padding-bottom:5px;">
          <div class="">
            <span style="padding-right:20px;margin-top:10px;">国家区域 ：</span>
            <Tag checkable color="blue">全部</Tag>
            <Tag checkable :checked="false" color="blue">标签一</Tag>
            <Tag checkable :checked="false" color="blue">标签二</Tag>
            <Tag checkable :checked="false" color="blue">标签三</Tag>
            <Tag checkable :checked="false" color="blue">标签四</Tag>
            <span class="moreselect">
              <Poptip placement="bottom" width="800" v-model="CountryAreaPoptipModal">
                <Button type="dashed" size="small">更多 +</Button>
                <div class="api" slot="content">
                  <div class="">
                    <Tabs v-model="CountryAreaTab" type="card">
                      <TabPane :label="Area.title" :key="key" :name="'key'+key" v-for="(Area, key) in CountryAreaList">
                        <CountryAreaTabPaneContent :AreaList="Area.list" @on-change="checkAllGroupChangeForCountryArea" :PickCountryArea="PickCountryArea" />
                      </TabPane>
                    </Tabs>
                  </div>
                  <div class="pickCountryAreaLabel" v-show="PickCountryArea.length>0">
                    <p>已选：</p>
                    <Tag type="border" closable color="blue" :key="key" :name="item" @on-close="closePickCountryArea" v-for="(item ,key) in PickCountryArea">{{item}}</Tag>
                  </div>
                  <div class="" style="margin-top:20px;text-align: center;">
                    <Button type="success">确定</Button>
                    <Button type="ghost" style="margin-left: 8px" @click="cancelPickCountryArea">取消</Button>
                  </div>
                </div>
              </Poptip>
            </span>
          </div>
          <div class="" style="margin-top:5px;">
            <span style="padding-right:20px;">订单规则 ：</span>
            <Tag checkable color="blue">全部</Tag>
            <Tag checkable :checked="false" color="blue">标签一</Tag>
            <Tag checkable :checked="false" color="blue">标签二</Tag>
            <Tag checkable :checked="false" color="blue">标签三标签三标签三标签三</Tag>
            <Tag checkable :checked="false" color="blue">标签四</Tag>
          </div>
        </div>
        <div class="" slot="content" style="padding-left:10px;border-top:1px #e9eaec solid;padding-top:5px;padding-bottom:5px;">
          <div class="" style="margin-top:5px;">
            <span style="padding-right:20px;">排序方式 ：</span>
            <Tag checkable color="blue">全部</Tag>
            <Tag checkable :checked="false" color="blue">标签一</Tag>
            <Tag checkable :checked="false" color="blue">标签二</Tag>
            <Tag checkable :checked="false" color="blue">标签三标签三标签三标签三标签三</Tag>
            <Tag checkable :checked="false" color="blue">标签四</Tag>
          </div>
        </div>
      </Panel>
    </Collapse>
    <div class="" style="position: absolute;right: 20px;">
      <Affix :offset-top="50">
        <Collapse v-model="value1" style="margin-left:30px;width:350px">
          <Panel name="1">
            工具栏
            <div slot="content" style="margin-left:10px;">
              <table class="toolbar-table">
                <tr>
                  <td>
                    <div class="toolbar-cell">
                      <Button type="primary">批量审核</Button>
                    </div>
                  </td>
                  <td>
                    <div class="toolbar-cell">
                      <Dropdown>
                        <Button type="primary">
                              批量操作
                              <Icon type="arrow-down-b"></Icon>
                            </Button>
                        <DropdownMenu slot="list">
                          <DropdownItem>驴打滚</DropdownItem>
                          <DropdownItem>炸酱面</DropdownItem>
                          <DropdownItem disabled>豆汁儿</DropdownItem>
                          <DropdownItem>冰糖葫芦</DropdownItem>
                          <DropdownItem divided>北京烤鸭</DropdownItem>
                        </DropdownMenu>
                      </Dropdown>
                    </div>
                  </td>
                </tr>
                <tr>
                  <td>
                    <div class="toolbar-cell">
                      <Dropdown>
                        <Button type="primary">
                              批量操作
                              <Icon type="arrow-down-b"></Icon>
                            </Button>
                        <DropdownMenu slot="list">
                          <DropdownItem>驴打滚</DropdownItem>
                          <DropdownItem>炸酱面</DropdownItem>
                          <DropdownItem disabled>豆汁儿</DropdownItem>
                          <DropdownItem>冰糖葫芦</DropdownItem>
                          <DropdownItem divided>北京烤鸭</DropdownItem>
                        </DropdownMenu>
                      </Dropdown>
                    </div>
                  </td>
                  <td>
                    <div class="toolbar-cell">
                      <Button type="warning">同步订单</Button>
                    </div>
                  </td>
                </tr>
                <tr>
                  <td>
                    <div class="toolbar-cell">
                      <Button type="error">标记黑名单</Button>
                    </div>
                  </td>
                </tr>
              </table>
            </div>
          </Panel>
        </Collapse>
        <div class="toolbar-page">
          <Page :total="40" size="small" show-elevator show-sizer show-total></Page>
        </div>
      </Affix>
    </div>
  </div>
  <br/>
  <tbl :orderList="orderList" />
</div>
</template>
<script>
import tbl from './table'
import CountryAreaTabPaneContent from './components/CountryAreaTabPaneContent'
export default {
  components: {
    tbl,
    CountryAreaTabPaneContent
  },
  data() {
    return {
      /* 国家区域 */
      CountryAreaTab: 'key0',
      PickCountryArea: [],
      CountryAreaPoptipModal:false,

      /* 订单数据 */
      orderList:[{
        ordersn: '20155454545454',
        contact: '小明',
        address: '地址1',
        address2: '地址2',
        city: '城市',
        province: '省/州',
        country: '国家',
        goodsname: '名称sku',
        goodsattr: '属性',
        goodscount: '数量',
        goodsprice: '单价',
        ordercomment: '订单备注',
        orderprice: 50000,
        ordercreatetime: '2017-04-04 04:04:04',
        orderpaytime: '2017-04-04 04:04:04',
      },{
        ordersn: '20155454545454',
        contact: '小明',
        address: '地址1',
        address2: '地址2',
        city: '城市',
        province: '省/州',
        country: '国家',
        goodsname: '名称sku',
        goodsattr: '属性',
        goodscount: '数量',
        goodsprice: '单价',
        ordercomment: '订单备注',
        orderprice: 50000,
        ordercreatetime: '2017-04-04 04:04:04',
        orderpaytime: '2017-04-04 04:04:04',
      },{
        ordersn: '20155454545454',
        contact: '小明',
        address: '地址1',
        address2: '地址2',
        city: '城市',
        province: '省/州',
        country: '国家',
        goodsname: '名称sku',
        goodsattr: '属性',
        goodscount: '数量',
        goodsprice: '单价',
        ordercomment: '订单备注',
        orderprice: 50000,
        ordercreatetime: '2017-04-04 04:04:04',
        orderpaytime: '2017-04-04 04:04:04',
      },],

      value: "1",
      value1: "1",
      CountryAreaList: [{
        title: '欧洲',
        count: 30,
        list: [{
          countryId: 17,
          countryNameCN: '安道尔1',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔2',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔3',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔4',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔5',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔6',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔7',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }]
      },{
        title: '亚洲',
        count: 30,
        list: [{
          countryId: 17,
          countryNameCN: '安尔1',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安尔2',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔3',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔4',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔5',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔6',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }, {
          countryId: 17,
          countryNameCN: '安道尔7',
          countryNameEbay: 'ANDORRA',
          countryNameEn: 'ANDORRA',
          currency: 'USD'
        }]
      }],
    }
  },
  methods: {
    checkAllGroupChangeForCountryArea(data){
      if(data[1]>-1){
        this.PickCountryArea.splice(data[1], 1)
      }else{
        this.PickCountryArea.push(data[0])
      }
    },
    cancelPickCountryArea(){
      this.CountryAreaPoptipModal = false;
    },
    closePickCountryArea(event, name){
      const i = this.PickCountryArea.indexOf(name)
      if(i>-1){
        this.PickCountryArea.splice(i, 1)
      }
    },
  }
}
</script>

<style>
.headbar {
  display: flex;
}

.headbar .ivu-collapse-content-box {
  padding-top: 3px !important;
  padding-bottom: 3px !important;
}

.toolbar-table .ivu-select-dropdown,
.toolbar-page .ivu-select-dropdown {
  left: inherit !important;
}

.toolbar-table td {
  width: 110px;
}

.toolbar-cell {
  margin-bottom: 5px;
}

.toolbar-cell .ivu-btn {
  width: 100px;
}

.toolbar-page {
  margin-left: 30px;
  margin-top: 30px;
  width: 450px;
}

.moreselect .ivu-checkbox-wrapper {
  width: 65px;
  line-height: 30px;
}
.pickCountryAreaLabel{
  border-top:1px #dddee1 solid;
  padding-top:20px;
  margin-top:10px;
  white-space: normal;
  height: 150px;
  overflow: auto;
}
</style>
