<!-- 视频教程 -->
<template>
  <div>
    <van-nav-bar :title="'机构政策'" left-arrow fixed @click-left="onClickLeft"/>
    <div class="main">
      <van-divider dashed :style="{ borderColor: '#aaa' }"><h4>东风联盟生活运营服务机构政策</h4></van-divider>
      <ul>
        <li>1、申请成立机构需要100㎡以上的办公场地，配套基础办公设备、茶室、会议室。</li>
        <li>2、申请人具有法人资格和公司主体。</li>
        <li>3、设立机构的目的，为当地代理商和用户提供培训服务，负责东风联盟生活在当地的品牌宣传，维护东风联盟生活在当地的市场秩序。</li>
        <li>4、机构在享有东风联盟生活三级分润制度和三级奖励制度、顶级代理底薪制度和顶级团队管理奖制度的基础上，给予运营服务机构最高还款交易流水无限代万2的运营补贴。</li>
        <li>5、总部给予机构资源支持，拨打400电话咨询的用户和代理推荐到当地机构。</li>
        <li>6、总部为机构商组织专项培训支持，优秀机构配套行销品物料支持。</li>
      </ul>
      <div class="organization">
        <van-divider dashed :style="{ borderColor: '#aaa' }"><h4>加入成为合作伙伴</h4></van-divider>
        <div class="long"></div>
        <ul>
      
        </ul>
      </div>
      <div class="needInformation">
        <van-divider dashed :style="{ borderColor: '#aaa' }"><h4>运营机构需提供基本资料</h4></van-divider>
        <div class="scroll">
          <table border="1" cellspacing="0" cellpadding="0">
            <thead>
            <th>序号</th>
            <th>文档名称</th>
            <th>份数</th>
            <th>是否必须</th>
            <th>盖章</th>
            <th>说明</th>
            </thead>
            <tbody>
            <tr>
              <td>1</td>
              <td>营业执照（副本）</td>
              <td>3份</td>
              <td class="color-red">必须</td>
              <td>复印件加盖公章</td>
              <td>需有效期内</td>
            </tr>
            <tr>
              <td>2</td>
              <td>组织机构代码（副本）</td>
              <td>3份</td>
              <td class="color-red">必须</td>
              <td>复印件加盖公章</td>
              <td>需有效期内</td>
            </tr>
            <tr>
              <td>3</td>
              <td>国、地税登记证（副本）</td>
              <td>3份</td>
              <td class="color-red">必须</td>
              <td>复印件加盖公章</td>
              <td>需有效期内</td>
            </tr>
            <tr>
              <td>4</td>
              <td>银行开户许可证</td>
              <td>1份</td>
              <td class="color-red">必须</td>
              <td>复印件加盖公章</td>
              <td></td>
            </tr>
            <tr>
              <td>5</td>
              <td>法定代表人身份证</td>
              <td>1份</td>
              <td class="color-red">必须</td>
              <td>复印件签字</td>
              <td>正反面彩色扫描件</td>
            </tr>
            <tr>
              <td>6</td>
              <td>ICP域名备案证明</td>
              <td>1份</td>
              <td class="color-green">可选</td>
              <td>复印件加盖公章</td>
              <td>请登录政府官方网站打印详情页，并加盖公章</td>
            </tr>
            <tr>
              <td>7</td>
              <td>提供3张经营场所照片</td>
              <td>1份</td>
              <td class="color-red">必须</td>
              <td>复印件加盖公章</td>
              <td>1张应挂有公司商标和全名，2张为营业场所全景。</td>
            </tr>
            <tr>
              <td>8</td>
              <td>场地租赁合同</td>
              <td>1份</td>
              <td class="color-red">必须</td>
              <td>复印件加盖公章</td>
              <td>需在租赁期内</td>
            </tr>
            </tbody>
          </table>
        </div>
        <p class="color-red">注：基本资料签约时提供</p>
      </div>
      <div class="erwei">
        <img width="200px" src="https://cader-install.oss-cn-shanghai.aliyuncs.com/backManage/erweima.jpg">
        <p>东风联盟生活官方微信服务号</p>
      </div>
    </div>
  </div>

</template>

<script>
import '@/assets/kade/gongzhong.less' //禁止复制
import {NavBar, PullRefresh, Cell, CellGroup, Divider} from 'vant';
import {newsQuery} from '@/api/showBrand'

export default {
  data() {
    return {
      fuwuList: [],
      brandId: this.global.brandId,
      isLoading: false,
      userId: '',
    };
  },
  components: {
    [NavBar.name]: NavBar,
    [PullRefresh.name]: PullRefresh,
    [Cell.name]: Cell,
    [CellGroup.name]: CellGroup,
    [Divider.name]: Divider
  },
  created() {
    this.userId = localStorage.getItem('userId')
    this.phone = localStorage.getItem('phone')
    this.token = localStorage.getItem('token')
    this.getNewsList()
  },
  beforeRouteEnter(to, from, next) {
    sessionStorage.setItem('routerFrom', from.name)
    next();
  },
  methods: {
    // 下拉刷新
    onRefresh() {
      setTimeout(() => {
        // this.$toast('刷新成功');
        this.getNewsList()
        this.isLoading = false;
      }, 1000);
    },
    onClickLeft() {
      window.history.back()
      return
      let name = sessionStorage.getItem('routerFrom')
      if (name == 'null' || name == 'link') {
        this.$router.push({name: 'home'})
      } else {
        this.$router.push({name: name})
      }
    },
    // 获取平台新闻分类数据
    getNewsList() {
      newsQuery(this.brandId, '使用说明').then(res => {
        if (res.resp_code == '000000') {
          this.fuwuList = res.result.content
        } else {
          this.$toast({message: res.resp_message, position: 'bottom'})
        }
      })
    },
    link(title) {
      let num = 0
      this.fuwuList.map(item => {
        if (item.title == title) {
          this.$router.push({
            name: 'appLink',
            params: {url: JSON.stringify(item.content), title: JSON.stringify(item.title), type: '8'}
          })
          return;
        } else {
          num++;
        }
      })
      if (num == this.fuwuList.length) {
        this.$toast({message: '敬请期待', position: 'bottom'})
      }
    },
    gonext(item) {
      this.$router.push({name: 'link', params: {url: JSON.stringify(item.content), title: JSON.stringify(item.title)}})
    }
  }
}

</script>
<style scoped lang='less'>
.main {
  padding-top: 45px;
  background-color: #fff;
  font-size: 14px;
  padding: 10px;
  font-family: '微软雅黑';
  color: rgb(48, 48, 48);

  h4 {
    text-align: center;
    font-size: 20px;
    margin: 10px 0px;
  }

  ul {
    margin: 0px 5px;

    li {
      padding: 3px;

      ul {
        padding-left: 25px;

        li {
          padding: 0px;
          list-style: outside;
        }
      }
    }

  }
}

.organization {
  margin-top: 15px;
  position: relative;

  ul {
    li {
      margin: 30px;

      img {
        display: inline-block;
        width: 40px;
        position: absolute;
        z-index: 10;
      }

      h3 {
        margin-left: 70px;
        margin-top: 10px;
        display: inline-block;
        width: 200px;
        color: #aaa;
        font-size: 14px;
      }
    }
  }

  .long {
    z-index: 0;
    position: absolute;
    left: 58px;
    top: 80px;
    border: 0.5px solid #aaa;
    width: 0px;
    height: 270px;
  }
}

.needInformation {
  margin-top: 15px;

  .scroll {
    overflow: scroll;
  }

  table {
    width: 550px;

    th, td {
      padding: 5px;
    }

    tbody {
      tr {
        td {

          &:last-child {
            width: 120px;
          }
        }

      }
    }
  }

  .color-red {
    color: rgb(255, 13, 13);
  }

  .color-green {
    color: rgb(19, 150, 19);
  }

  table, table thead th, table tr td {
    border: 1px solid #aaa;
    font-weight: 500;
    text-align: left;
  }
}

.erwei {
  width: 100%;
  padding: 20px 20px;
  text-align: center;
}


</style>
