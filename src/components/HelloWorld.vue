<template>
    <div class="menu">
      <div class="cover" :class="[filter.selected!=''?'':'invisible']"></div>
      <div class="filter fixed">
          <!-- 一级菜单开始 -->
          <div class="fmenu">
            <div :class="{cf:true, active:cfName !='吃饭'}" class="flex">
              <div class="sn" :class="[filter.selected=='cf'?'open':'close']" @click="switchFilter" data-name="cf">{{cfName}}</div>
            </div>
            <div :class="{sj:true,active:sjName !='睡觉'}" class="flex">
              <div class="sn" :class="[filter.selected=='sj'?'open':'close']" @click="switchFilter" data-name="sj">{{sjName}}</div>
            </div>
            <div :class="{dd:true,active:ddName !='打豆豆'}" class="flex">
              <div class="sn" :class="[filter.selected=='dd'?'open':'close']" @click="switchFilter" data-name="dd">{{ddName}}</div>
            </div>
          </div>
          <!-- 一级菜单结束 -->
          <!-- 二级菜单开始 -->
          <div class="fkind" :class="[filter.selected==''?'invisible':'']">
            <div :class="[filter.selected=='cf'?'':'invisible']" class="item-cf">
              <div class="tabs">
                <div :class="{zc:true,on:filter.secondTab=='zc'}" data-name='zc' @click="secondTab" >中餐</div>
                <div :class="{xc:true,on:filter.secondTab=='xc'}" data-name='xc' @click="secondTab" >西餐</div>
              </div>
              <div class="tab-zc" :class="[filter.secondTab=='zc'?'xs':'yc']" v-if="filter.secondTab=='zc'">
                <div class="left" >
                  <div :data-text="item.name" :data-id="item.id" :class="{active:item.id==filter.threeTabId}" @click="threeTab" v-for="(item,index) in zcs " :key="index">{{item.name}}</div>
                </div>
                <div class="right" v-for="(item,index) in zcm" v-if="item.id==filter.threeTabId" :key="index" >
                  <div class="cm" v-for="(t,i) in item.name" :key="i" @click="dosomething" >
                    {{t}}
                  </div>
                </div>
              </div>
            </div>
          </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      filter:{
        selected:'',//一级模块;
        secondTab:'zc',//现有默认;
        threeTabId:''
      },
      zcs:[
        {
          id:1,
          name:'河南'
        },
        {
          id:2,
          name:'四川'
        },
        {
          id:3,
          name:'河北'
        }
      ],
      xcg:['美国','英国','加拿大'],
      zcm:[
        {
          id:1,
          name:['馒头','烩面','胡辣汤']
        },
        {
          id:2,
          name:['麻婆豆腐','辣椒炒肉','火锅']
        },
        {
          id:3,
          name:['驴肉火烧','酱汁瓦块鱼','大饼']
        }
      ]
    }
  },
  computed:{
    cfName(){
      let result='吃饭';
      return result;
    },
    sjName(){
      let result='睡觉';
      return result;
    },
    ddName(){
      let result='打豆豆';
      return result;
    }
  },
  methods:{
    // 一级菜单
    switchFilter(e){
      let name=e.currentTarget.dataset.name;
      if(this.filter.selected == name){
        name = '';
      }
      this.filter.selected = name;
    },
    // 二级菜单tab栏;
    secondTab(e){
      let name=e.currentTarget.dataset.name;
      this.filter.secondTab = name;
    },
    // 三级菜单;
    threeTab(e){
      let id=e.currentTarget.dataset.id;
      this.filter.threeTabId=id;
    },
    dosomething(e){
      let id=e.currentTarget.dataset.id;
      let name=e.currentTarget.dataset.name;
      this.filter.selected='';
      alert('头痛！')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
  .filter{
    .fmenu{
      display: flex;
      text-align: center;
    }
    .flex{
      flex: 1;
    };
    .sn.open{
      background-color: pink;
    }
    .invisible{
      display: none;
    }
    .fkind{
      padding-top: 1.333333rem;
    }
    .tabs{
      display: flex;
      .on{
        background-color: green;
      };
      div{
        flex:1;
        text-align: center;
      };
      
    }
    .tab-zc{
      padding-top: 1.333333rem;
      display: flex;
      .left{
        flex:1;
      };
      .right{
        flex: 1;
      }
    }
    .active{
      background-color: pink;
    }
  }
  .cover{
      background-color: rgba(0,0,0,.2);            
      position: fixed;            
      bottom: 0;
      right: 0;
      left: 0;
      top: 0;
      z-index: 4;
      &.invisible {
        display: none;
      } 
    }
    .fixed{
      background-color: #fff;
      width: 100%;
      position: fixed;
      top: 0;
      z-index: 9999;
    }
</style>
