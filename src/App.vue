<template>
  <div id="app">
    <el-container style="border: 1px solid #eee">
      <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
        <el-menu
                default-active="3"
                class="el-menu-vertical-demo"
        >
          <el-menu-item index="1" @click="changeInfo(3)">
            <i class="el-icon-menu"></i>
            <span slot="title">投资类</span>
          </el-menu-item>
          <el-menu-item index="2" @click="changeInfo(4)">
            <i class="el-icon-document"></i>
            <span slot="title">其他类</span>
          </el-menu-item>
          <el-submenu index="3">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>模板分类</span>
            </template>
            <el-menu-item-group>
              <template slot="title">活期类</template>
              <div @click="changeInfo(0,$event)">
                <el-menu-item index="1-1" >PrdTempINI004</el-menu-item>
                <el-menu-item index="1-2" >PrdTempINI006</el-menu-item>
                <el-menu-item index="1-3" >PrdTempINI012</el-menu-item>
                <el-menu-item index="1-4" >PrdTempINI101</el-menu-item>
                <el-menu-item index="1-5" >PrdTempINI102</el-menu-item>
                <el-menu-item index="1-6" >PrdTempINI110</el-menu-item>
                <el-menu-item index="1-7" >PrdTempINI111</el-menu-item>
                <el-menu-item index="1-8" >PrdTempINI113</el-menu-item>
                <el-menu-item index="1-9" >新增模板</el-menu-item>
              </div>
            </el-menu-item-group>
            <el-menu-item-group >
              <template slot="title">定期类</template>
              <div @click="changeInfo(1,$event)">
                <el-menu-item index="2-1">PrdTempINI007</el-menu-item>
                <el-menu-item index="2-2">PrdTempINI008</el-menu-item>
                <el-menu-item index="2-3">PrdTempINI013</el-menu-item>
                <el-menu-item index="2-4">PrdTempINI103</el-menu-item>
                <el-menu-item index="2-5">PrdTempINI104</el-menu-item>
                <el-menu-item index="2-6">PrdTempINI105</el-menu-item>
                <el-menu-item index="2-7">PrdTempINI106</el-menu-item>
                <el-menu-item index="2-8">PrdTempINI107</el-menu-item>
                <el-menu-item index="2-9">PrdTempINI108</el-menu-item>
                <el-menu-item index="2-10">PrdTempINI109</el-menu-item>
                <el-menu-item index="2-11">新增模板</el-menu-item>
              </div>
            </el-menu-item-group>
            <el-menu-item-group>
              <template slot="title">基金类</template>
              <div @click="changeInfo(2,$event)">
                <el-menu-item index="3-1">PrdTempINI001</el-menu-item>
                <el-menu-item index="3-2">PrdTempINI002</el-menu-item>
                <el-menu-item index="3-3">PrdTempINI003</el-menu-item>
                <el-menu-item index="3-4">PrdTempINI009</el-menu-item>
                <el-menu-item index="3-5">其他模板</el-menu-item>
              </div>
            </el-menu-item-group>
          </el-submenu>

          <el-menu-item index="4" disabled>
            <i class="el-icon-setting"></i>
            <span slot="title">未知分类</span>
          </el-menu-item>
        </el-menu>
      </el-aside>

      <el-container>
        <el-main>
          <div class="left">
            左侧区域:
            <div class="l_section"><el-input v-model="infoData.leftText" placeholder="左侧文案"></el-input></div>
            <div class="l_section">
              <el-select v-model="infoData.leftFiled" placeholder="展示字段">
                <el-option
                        v-for="item in FiledList"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                </el-option>
              </el-select>
            </div>
            <div class="l_section">
              <el-select v-model="infoData.leftAddSign" placeholder="有无正负号">
                <el-option
                        v-for="item in addPlugin"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                </el-option>
              </el-select>
            </div>
            <div class="l_section">
              <el-select v-model="infoData.leftUnit" placeholder="单位">
                <el-option
                        v-for="item in unit"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                </el-option>
              </el-select>
            </div>
          </div>
          <div class="right">
            右侧区域:
            <div class="l_section"><el-input v-model="infoData.rightText" placeholder="右侧文案"></el-input></div>
            <div class="l_section">
              <el-select v-model="infoData.rightFiled" placeholder="展示字段">
                <el-option
                        v-for="item in FiledList"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                </el-option>
              </el-select>
            </div>
            <div class="l_section">
              <el-select v-model="infoData.rightAddSign" placeholder="有无正负号">
                <el-option
                        v-for="item in addPlugin"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                </el-option>
              </el-select>
            </div>
            <div class="l_section">
              <el-select v-model="infoData.rightUnit" placeholder="单位">
                <el-option
                        v-for="item in unit"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                </el-option>
              </el-select>
            </div>
          </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      FiledList: [{
        value: 'accountId',
        label: '理财账号',
      }, {
        value: 'carryoverIncome',
        label: '收益'
      }, {
        value: 'customerLevel',
        label: '客户等级'
      }, {
        value: 'expectIncome',
        label: '预期收益'
      }, {
        value: 'expectedTimeOfArrival',
        label: '预计到账日期'
      },{
        value: 'expireDay',
        label: '到期日'
      },{
        value: 'expireDayFlag',
        label: '到期日的标识'
      },{
        value: 'expireDays',
        label: '还有多少天到期'
      },{
        value: 'fundType',
        label: '基金类型'
      },{
        value: 'holdPrincipal',
        label: '持有本金'
      },{
        value: 'productAmount',
        label: '持有金额'
      },{
        value: 'productCode',
        label: '产品代码'
      },{
        value: 'productId',
        label: '产品id'
      },{
        value: 'productName',
        label: '产品名称'
      },{
        value: 'productShare',
        label: '持有份额'
      },{
        value: 'productType',
        label: '产品类型'
      },{
        value: 'promptFlag',
        label: '提示规划信息'
      },{
        value: 'sellCode',
        label: '销售商代码'
      },{
        value: 'showFundReviewFlag',
        label: '是否展示基金点评字段'
      },{
        value: 'startDate',
        label: '首发确认日'
      },{
        value: 'taShortName',
        label: '产品简称'
      },{
        value: 'totIncomeOrProfit',
        label: '累计收益/浮动盈亏'
      },{
        value: 'yesIncome',
        label: '昨日收益/昨日盈亏'
      },],
      addPlugin:[{
        value: false,
        label: '无正负号'
      },{
        value: true,
        label: '有正负号'
      }],
      unit:[{
        value:'0',
        label:'无单位'
      },{value:'1',
        label:'份'
      },{value:'2',
          label:'金额单位'
      },],
      infoData:{
        leftText:'待分配收益',
        leftFiled:'totIncomeOrProfit',
        leftAddSign:true,
        leftUnit:'2',
        rightText:'累计收益',
        rightFiled:'taShortName',
        rightAddSign:false,
        rightUnit:'0'
      },
      manageList:{
        group_invest:{
          leftText:'持仓份额',
          leftFiled:'productShare',
          leftAddSign:false,
          leftUnit:'1',
          rightText:'',
          rightFiled:'',
          rightAddSign:false,
          rightUnit:'0'
        },
        group_other:{
          leftText:'持仓份额',
          leftFiled:'productShare',
          leftAddSign:false,
          leftUnit:'1',
          rightText:'',
          rightFiled:'',
          rightAddSign:false,
          rightUnit:'0'
        },
        group_list:{
          // 活期类
          PrdTempINI004:{
            leftText:'昨日收益',
            leftFiled:'yesIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI006:{
            leftText:'昨日收益',
            leftFiled:'yesIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI012:{
            leftText:'昨日收益',
            leftFiled:'yesIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI101:{
            leftText:'待分配收益',
            leftFiled:'carryoverIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI102:{
            leftText:'待分配收益',
            leftFiled:'carryoverIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI110:{
            leftText:'持有越久,收益越高',
            leftFiled:'',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'',
            rightFiled:'',
            rightAddSign:false,
            rightUnit:'0'
          },
          PrdTempINI111:{
            leftText:'待分配收益',
            leftFiled:'carryoverIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI113:{
            leftText:'待分配收益',
            leftFiled:'carryoverIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:false,
            rightUnit:'2'
          },
          // 定期类
          PrdTempINI007:{
            leftText:'到期日',
            leftFiled:'expireDay',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'预期收益',
            rightFiled:'expectIncome',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI008:{
            leftText:'',
            leftFiled:'',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'',
            rightFiled:'',
            rightAddSign:false,
            rightUnit:'0'
          },
          PrdTempINI013:{
            leftText:'到期日',
            leftFiled:'expireDay',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'预期收益',
            rightFiled:'expectIncome',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI103:{
            leftText:'到期日',
            leftFiled:'expireDay',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'预期收益',
            rightFiled:'expectIncome',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI104:{
            leftText:'到期日',
            leftFiled:'expireDay',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'预期收益',
            rightFiled:'expectIncome',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI105:{
            leftText:'首次确认日',
            leftFiled:'startDate',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'',
            rightFiled:'',
            rightAddSign:false,
            rightUnit:'0'
          },
          PrdTempINI106:{
            leftText:'到期日',
            leftFiled:'expireDay',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'预期收益',
            rightFiled:'expectIncome',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI107:{
            leftText:'到期日',
            leftFiled:'expireDay',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'预期收益',
            rightFiled:'expectIncome',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI108:{
            leftText:'到期日',
            leftFiled:'expireDay',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'预期收益',
            rightFiled:'expectIncome',
            rightAddSign:false,
            rightUnit:'2'
          },
          PrdTempINI109:{
            leftText:'持有越久,收益越高',
            leftFiled:'',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'',
            rightFiled:'',
            rightAddSign:false,
            rightUnit:'0'
          },
          // 基金类
          PrdTempINI001:{
            leftText:'昨日收益/昨日盈亏',
            leftFiled:'yesIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益/累计盈亏',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:true,
            rightUnit:'2'
          },
          PrdTempINI002:{
            leftText:'昨日收益/昨日盈亏',
            leftFiled:'yesIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益/累计盈亏',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:true,
            rightUnit:'2'
          },
          PrdTempINI003:{
            leftText:'昨日收益/昨日盈亏',
            leftFiled:'yesIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益/累计盈亏',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:true,
            rightUnit:'2'
          },
          PrdTempINI009:{
            leftText:'昨日收益/昨日盈亏',
            leftFiled:'yesIncome',
            leftAddSign:true,
            leftUnit:'2',
            rightText:'累计收益/累计盈亏',
            rightFiled:'totIncomeOrProfit',
            rightAddSign:true,
            rightUnit:'2'
          },
          // 新模板
          prdTempINI_new:{
            leftText:'',
            leftFiled:'',
            leftAddSign:false,
            leftUnit:'0',
            rightText:'',
            rightFiled:'',
            rightAddSign:false,
            rightUnit:'0'
          }
        }
      }
    }
  },
  methods:{
    changeInfo(group,event){
      if(event){
        debugger;
        var tplId = event.target.innerText;
      }
      if(group === 3){
        debugger;
        this.infoData=Object.assign({},this.infoData,this.manageList.group_invest);
      }else if(group === 4){
        this.infoData=Object.assign({},this.infoData,this.manageList.group_invest);
      }else{
        switch(tplId){
          case 'PrdTempINI004':
          case 'PrdTempINI006':
          case 'PrdTempINI012':
          case 'PrdTempINI101':
          case 'PrdTempINI102':
          case 'PrdTempINI110':
          case 'PrdTempINI111':
          case 'PrdTempINI113':
          case 'PrdTempINI007':
          case 'PrdTempINI008':
          case 'PrdTempINI013':
          case 'PrdTempINI103':
          case 'PrdTempINI104':
          case 'PrdTempINI105':
          case 'PrdTempINI106':
          case 'PrdTempINI107':
          case 'PrdTempINI108':
          case 'PrdTempINI109':
          case 'PrdTempINI001':
          case 'PrdTempINI002':
          case 'PrdTempINI003':
          case 'PrdTempINI009':
            this.infoData=Object.assign({},this.infoData,this.manageList.group_list[tplId]);
            break;
          default:
            this.infoData=Object.assign({},this.infoData,this.manageList.group_list.prdTempINI_new);
            break;
        }
      }
    }
  }

}
</script>

<style>
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
  }

  .el-aside {
    color: #333;
  }
  #app{
    font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  }
  .left{
    border: 1px solid #eee;
    padding: 10px;
  }
  .right{
    border: 1px solid #eee;
    padding: 10px;
    margin-top: 20px;
  }
  .l_section{
    margin-top: 10px;
  }
</style>
