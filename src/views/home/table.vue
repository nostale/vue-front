<template>
<div class="ivu-table-wrapper" style="width:1300px">
  <div class="ivu-table ivu-table-border">
    <div class="ivu-table-header">
      <table cellspacing="0" cellpadding="0" border="0" style="width: 1299px;">
        <colgroup>
          <col width="60">
          <col width="162">
          <col width="162">
          <col width="163">
          <col width="163">
          <col width="253">
          <col width="163">
          <col width="163">
        </colgroup>
        <thead>
          <tr>
            <th class="ivu-table-column-center">
              <div class="ivu-table-cell">
                <Checkbox @on-change="CheckAllDataList"></Checkbox>
              </div>
            </th>
            <th class="">
              <div class="ivu-table-cell"><span>Name</span>
              </div>
            </th>
            <th class="">
              <div class="ivu-table-cell"><span>Age</span>
              </div>
            </th>
            <th class="">
              <div class="ivu-table-cell"><span>Address</span>
              </div>
            </th>
            <th class="">
              <div class="ivu-table-cell"><span>Name</span>
              </div>
            </th>
            <th class="">
              <div class="ivu-table-cell"><span>Age</span>
              </div>
            </th>
            <th class="">
              <div class="ivu-table-cell"><span>Address</span>
              </div>
            </th>
            <th class="">
              <div class="ivu-table-cell"><span>Address</span>
              </div>
            </th>
          </tr>
        </thead>
      </table>
    </div>
    <div class="ivu-table-body" v-show="orderList.length>0">
      <table cellspacing="0" cellpadding="0" border="0" style="width: 1299px;">
        <colgroup>
          <col width="60">
          <col width="162">
          <col width="162">
          <col width="163">
          <col width="163">
          <col width="253">
          <col width="163">
          <col width="163">
        </colgroup>
        <tbody class="ivu-table-tbody" v-for="(item, key) in orderList">
          <tr class="ivu-table-row tr-head">
            <td class="ivu-table-column-center td-head">
              <div class="ivu-table-cell">
                <Checkbox></Checkbox>
              </div>
            </td>
            <td class="td-head" colspan="4">
              <div class="ivu-table-cell">
                <span>BAOGUOHAO_XM1122</span>
                <span class="" style="margin-left:20px;" @click="ShowPoptip">
                  <Tooltip content="Top Center 文字提示" placement="top">
                    <div class="td-tag blue"></div>
                  </Tooltip>
                  <Tooltip content="Top Center 文字提示" placement="top">
                    <div class="td-tag green"></div>
                  </Tooltip>
                  <Tooltip content="Top Center 文字提示" placement="top">
                    <div class="td-tag red"></div>
                  </Tooltip>
                  <Tooltip content="Top Center 文字提示" placement="top">
                    <div class="td-tag yellow"></div>
                  </Tooltip>
                </span>
              </div>
            </td>
            <td class="td-head" colspan="2">
            </td>
            <td class="td-head">
              <div class="ivu-table-cell">
                <span>「手工订单」</span>
              </div>
            </td>
          </tr>
          <tr class="ivu-table-row">
            <td class="" colspan="2">
              <div class="ivu-table-cell">
                <div class="ivu-table-cell-info">
                  <div class="ivu-table-cell-info-img">
                    <Poptip trigger="hover" content="提示内容" placement="right">
                      <div class="poptip-img"><img style="width:60px;height:60px;" src="https://o5wwk8baw.qnssl.com/a42bdcc1178e62b4694c830f028db5c0/avatar" alt=""></div>
                      <div class="" slot="content">
                        <img src="https://o5wwk8baw.qnssl.com/a42bdcc1178e62b4694c830f028db5c0/avatar" alt="">
                      </div>
                    </Poptip>
                  </div>
                  <div class="ivu-table-cell-info-list">
                    <p>
                      <span style="font-size:14px;height:20px;vertical-align: middle;">{{item.goodsname}} * </span>
                      <Badge :count="item.goodscount"></Badge>
                    </p>
                    <p>USD {{item.goodsprice}}</p>
                    <p>{{item.goodsattr}}</p>
                  </div>
                </div>
              </div>
            </td>
            <td class="">
              <div class="ivu-table-cell">
                <span>{{item.orderprice}}</span>
              </div>
            </td>
            <td class="">
              <div class="ivu-table-cell">
                <span>{{item.contact}} 【{{item.country}}】</span>
              </div>
            </td>
            <td class="">
              <div class="ivu-table-cell">
                <Poptip trigger="hover">
                    <a>{{item.ordersn}}</a>
                    <div slot="content">
                        <a>复制</a>
                    </div>
                </Poptip>
              </div>
            </td>
            <td class="">
              <div class="ivu-table-cell">
                <p> 下单时间: {{item.ordercreatetime}}</p>
                <p> 付款时间: {{item.orderpaytime}}</p>
              </div>
            </td>
            <td class="">
              <div class="ivu-table-cell">
                <span>已付款</span>
              </div>
            </td>
            <td class="">
              <div class="ivu-table-cell">
                <a href="#">按钮1</a>
                <a href="#">按钮1</a>
                <a href="#">按钮1</a>
                <!-- <p><Button size="small">按钮1</Button></p>
                <p><Button size="small">按钮2</Button></p>
                <p><Button size="small">按钮2</Button></p> -->
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="ivu-table-tip" v-show="orderList.length<=0">
      <table cellspacing="0" cellpadding="0" border="0">
        <tbody>
          <tr>
            <td><span>暂无筛选结果</span></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
</template>
<script>
export default {
  props:{
    orderList:{
      type: Array,
      default: [],
    }
  },
  methods:{
    ShowPoptip(){
      render: (h, params) => {
        return h('Tag', {
            props: {
                type: 'dot',
                color: 'red'
            }
        }, 'text');
      }
    },
    CheckAllDataList(value){
      console.log(value);
    },
  }
}
</script>
<style scope>
  .td-head{
    border-right: none !important;
    height: 40px !important;
    background-color: #F2F2F2 !important;
  }
  .tr-head{
    font-size: 13px !important;
    padding: 5px 0 !important;
  }
  .td-tag{
    width: 20px;
    height: 20px;
    display: inline-block;
    vertical-align: middle;
    text-align: center;
    line-height: 20px;
    cursor: pointer;
    border-radius: 4px;
    margin-right: 1px;
    color: #FFF;
  }
  .blue{
    background-color: #2d8cf0;
  }
  .green{
    background-color: #19be6b;
  }
  .red{
    background-color: #ed3f14;
  }
  .yellow{
    background-color: #f90;
  }
  .ivu-table-cell-info{
    display: flex;

    margin-top: 10px;
    margin-bottom: 10px;
  }
  .poptip-img{
    padding:3px;
    height: 68px;
    width: 68px;
    border: 1px solid #cccccc;
  }
  .ivu-table-cell-info-list{
    margin-left: 10px;
  }
</style>
