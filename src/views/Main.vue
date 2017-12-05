<!--<style lang="less">
    @import "./main.less";
</style>
<template>
    <div class="main" :class="{'main-hide-text': shrink}">
        <div class="sidebar-menu-con" :style="{width: shrink?'60px':'200px', overflow: shrink ? 'visible' : 'auto'}">
            <shrinkable-menu
                :shrink="shrink"
                :menu-list="menuList">
                <div slot="top" class="logo-con">
                    <img v-show="!shrink"  src="../images/logo.jpg" key="max-logo" />
                    <img v-show="shrink" src="../images/logo-min.jpg" key="min-logo" />
                </div>
            </shrinkable-menu>
        </div>
        <div class="main-header-con" :style="{paddingLeft: shrink?'60px':'200px'}">
            <div class="main-header">
                <div class="navicon-con">
                    <Button :style="{transform: 'rotateZ(' + (this.shrink ? '-90' : '0') + 'deg)'}" type="text" @click="toggleClick">
                        <Icon type="navicon" size="32"></Icon>
                    </Button>
                </div>
                <div class="header-avator-con">
                    <div class="user-dropdown-menu-con">
                        <Row type="flex" justify="end" align="middle" class="user-dropdown-innercon">
                            <Dropdown transfer trigger="click" @on-click="handleClickUserDropdown">
                                <a href="javascript:void(0)">
                                    <span class="main-user-name">{{ userName }}</span>
                                    <Icon type="arrow-down-b"></Icon>
                                </a>
                                <DropdownMenu slot="list">
                                    <DropdownItem name="loginout" divided>退出登录</DropdownItem>
                                </DropdownMenu>
                            </Dropdown>
                            <Avatar icon="person" style="background: #619fe7;margin-left:10px;"></Avatar>
                        </Row>
                    </div>
                </div>
            </div>
        </div>
        <div class="single-page-con" :style="{left: shrink?'60px':'200px'}">
            <div class="single-page">
                <router-view></router-view>
            </div>menuList
        </div>
    </div>
</template>
<script>
import Cookies from 'js-cookie';
import shrinkableMenu from './main-components/shrinkable-menu/shrinkable-menu.vue';

export default {
    components: {
        shrinkableMenu
    },
    data () {
        return {
            shrink: false,
            userName: ''
        };
    },
    computed: {
        menuList () {
            return this.$store.state.app.menuList;
        }
    },
    methods: {
        init () {
            this.userName = Cookies.get('user');
        },
        toggleClick () {
            this.shrink = !this.shrink;
        },
        handleClickUserDropdown (name) {
            this.$router.push({
                name: 'login'
            });
        }
    },
    mounted () {
        this.init();
    }
};
</script>
-->

<style>
    .layout{
        border: 1px solid #d7dde4;
        background: #f5f7f9;
        overflow: hidden;
    }
    .layout-logo{
        width: 100px;
        height: 30px;
        background: #5b6270;
        border-radius: 3px;
        float: left;
        position: relative;
        top: 15px;
        left: 20px;
    }
    .layout-nav{
        margin-left: 200px;
    }
    .layout-assistant{
        margin-left: 200px;
        height: inherit;
    }
    .layout-content{
        width: 100%;
        min-height: 200px;
        overflow: hidden;
        background: #fff;
        border-radius: 4px;
        display: flex;
    }
    .layout-content-main{
        width: 100%;
    }
    .layout-content-main-breadcrumb{
        padding: 10px 15px 10px;
        border-bottom: 1px #dddee1 solid;
    }
    .layout-content-main-view{
        padding: 15px;
        width: 100%;
    }
    .layout-copy{
        text-align: center;
        padding: 10px 0 20px;
        color: #9ea7b4;
    }
    .ivu-menu-item-group>ul{
        display: flex;
    }
    .ivu-select-dropdown{
        left: -50px!important;
    }
    .layout-content-menu{
        min-width:200px;
        z-index: 1;
    }
    .layout-content-menu>ul{
        overflow: auto;
    }
</style>
<template>
    <div class="layout">
        <Menu mode="horizontal" :active-name="pickLeftMenuAN" theme="dark" @on-select="topMenu">
            <div class="layout-logo"></div>
            <div class="layout-nav" style="width: 100%;">
                <MenuItem name="home">
                    首页
                </MenuItem>
                <Submenu :name="key" :key="key" v-for="(item, key) in menuList">
                    <template slot="title">
                        <Icon :type="item.icon"></Icon>
                        {{item.name}}
                    </template>
                    <MenuGroup :title="child.name" :key="childkey" v-for="(child, childkey) in item.children">
                      <MenuItem :name="key+'-'+childkey+'-'+k" :key="k" v-for="(i, k) in child.children">{{i.name}}</MenuItem>
                    </MenuGroup>
                </Submenu>
            </div>
        </Menu>
        <div class="layout-content">
          <div class="layout-content-menu">
            <Menu ref="leftMenu" :active-name="pickLeftMenuAN" width="auto" :open-names="pickLeftMenuON" :style="menuHeight" @on-select="LeftMenu">
                <Submenu :name="pickNumber+'-'+key" :key="key" v-for="(item, key) in leftMenu.children">
                    <template slot="title">
                        <Icon :type="item.icon"></Icon>
                        {{item.name}}
                    </template>
                    <MenuItem :name="pickNumber+'-'+key+'-'+k" :key="k" v-for="(i, k) in item.children">{{i.name}}</MenuItem>
                </Submenu>
            </Menu>
          </div>
          <div class="layout-content-main">
              <div class="layout-content-main-breadcrumb">
                  <Breadcrumb>
                      <BreadcrumbItem href="#">Home</BreadcrumbItem>
                      <BreadcrumbItem href="#">Projects</BreadcrumbItem>
                      <BreadcrumbItem>iView</BreadcrumbItem>
                  </Breadcrumb>
              </div>
              <div class="layout-content-main-view">
                <router-view></router-view>
              </div>
          </div>
        </div>
        <div class="layout-copy">
            2011-2016 &copy; TalkingData
        </div>
        <BackTop></BackTop>
    </div>
</template>
<script>
    export default {
      created(){
        console.log(this.menuList);
      },
      data(){
        return {
          pickLeftMenuAN:'',
          pickLeftMenuON:[],
          pickNumber:0,
          leftMenu:[],
          menuList:[{
            key:'order',
            name:'导航一',
            icon:'stats-bars',
            path:'',
            children:[{
              key:'ordertitle',
              name:'头部导航二',
              icon:'',
              path:'',
              children:[{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              }]
            },{
              key:'ordertitle',
              name:'头部导航二',
              icon:'',
              path:'',
              children:[{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              }]
            }]
          },{
            key:'order',
            name:'导航一',
            icon:'stats-bars',
            path:'',
            children:[{
              key:'ordertitle',
              name:'头部导航二',
              icon:'',
              path:'',
              children:[{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              }]
            },{
              key:'ordertitle',
              name:'头部导航二',
              icon:'',
              path:'',
              children:[{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              }]
            },{
              key:'ordertitle',
              name:'头部导航二',
              icon:'',
              path:'',
              children:[{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              }]
            },{
              key:'ordertitle',
              name:'头部导航二',
              icon:'',
              path:'',
              children:[{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              },{
                key:'ordertitle',
                name:'头部导航三',
                icon:'',
                path:'',
              }]
            }]
          }],
          menuHeight:{
            height: document.documentElement.clientHeight  - 110 +'px',
            paddingTop: '20px',
          }
        }
      },
      methods: {
        topMenu(val){
          let pickMenu = val.split('-');
          this.pickLeftMenuAN = pickMenu[0]+'-'+pickMenu[1]+'-'+pickMenu[2];
          this.pickNumber = pickMenu[0]
          this.leftMenu = this.menuList[pickMenu[0]]
          this.pickLeftMenuON = [pickMenu[0]+'-'+pickMenu[1]]
          setTimeout(()=>{
            this.$nextTick(() => {
                this.$refs.leftMenu.updateOpened();
                this.$refs.leftMenu.updateActiveName()
            });
          })
        },
        LeftMenu(val){
          this.pickLeftMenuAN = val;
        }
      }
    }
</script>
