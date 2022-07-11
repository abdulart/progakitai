<template>
  <div class="page">
    <div class="page__hd">
      <div class="page__title">Dong Zheng</div>
      <div class="page__desc">
        Something about your app here
        Something about your app here
        Something about your app here
        Something about your app here
      </div>
    </div>
    <div class="page__bd page__bd_spacing">
      <div class="kind-list">
        <div v-for="(item1,index1) in list" :key="index1" class="card-custom-dz">
          <div class="kind-list__item">
            <div
              :id="item1.id"
              :class="{'kind-list__item-hd_show':item1.open}"
              class="weui-flex,kind-list__item-hd custom-list-class-pd"
              @click="kindToggle"
            >
              <div class="weui-flex__item custom-dz-list-head">{{item1.name}}</div>
              <img class="kind-list__img custom-dz-list-image" :src=" '/static/images/icon_nav_'+item1.id+'.png'" />
            </div>
            <div :class="{'kind-list__item-bd_show':item1.open}" class="kind-list__item-bd">
              <div :class="{'weui-cells_show':item1.open}" class="weui-cells">
                <navigator
                  v-for="(item2,index2) in item1.pages"
                  :key="index2"
                  class="weui-cell weui-cell_access menu-items-custom"
                  :url=" '/pages/' + item1.id + '/' + item2+'/'+'main' + '' "
                >
                  <div class="weui-cell__bd">
                      <text>{{item1['translate'][item2] || item2 }}</text>
                  </div>
                  <div class="weui-cell__ft">
                    <mp-badge :isShowBadge=false :dot=false :info=9 badgePos="right-top">
                      <button class="weui-btn mini-btn" type="normal" size="mini">&#x2192;</button>
                    </mp-badge>
                  </div>
                </navigator>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="weui-footer weui-footer_fixed-bottom">
        <p class="weui-footer__links">
            <a href="#" class="weui-footer__link weui-wa-hotarea">Dong Zheng</a>
        </p>
        <p class="weui-footer__text">Copyright &copy; 2022</p>
    </div>
  </div>
</template>

<script>
import mpButton from 'mpvue-weui/src/button';
import mpUploader from 'mpvue-weui/src/uploader';
import mpBadge from 'mpvue-weui/src/badge';
export default {
  data() {
    return {
      list: [
        {
          id: 'universities',
          name: '大學錄取',
          open: false,
          pages: ['apply', 'requests'],
          translate: {
            'apply': '申請',
            'requests': '要求'
          }
        },
        {
          id: 'homeworks',
          name: '家庭作業',
          open: false,
          pages: ['apply', 'requests'],
          translate: {
            'apply': '申請',
            'requests': '要求'
          }
        },
        {
          id: 'aboutus',
          name: '關於我們',
          open: false,
          pages: ['info', 'feedback'],
          translate: {
            'info': '信息',
            'feedback': '反饋和幫助'
          }
        }
      ]
    };
  },

  components: {
    mpButton,
    mpUploader,
    mpBadge
  },

  methods: {
    upLoadSuccess(e) {
      console.log(e)
    },
    testFunction(e) {
      console.log(e)
      wx.showLoading({
        title: 'Loading '
      })

      setTimeout(function () {
        wx.hideLoading()
      }, 2000)
    },
    kindToggle(e) {
      var id = e.currentTarget.id;
      var list = this.list;
      for (var i = 0, len = list.length; i < len; ++i) {
        if (list[i].id === id) {
          list[i].open = !list[i].open;
        } else {
          list[i].open = false;
        }
      }
      this.list = list;
    }
  },

  created() {
  }
};
</script>

<style scoped>
.menu-items-custom {
  border-left: 2px solid #ddd;
}

.menu-items-custom:hover {
  background: #ddd;
}
/*!
 * WeUI v1.1.1 (https://github.com/weui/weui-wxss)
 * Copyright 2019 Tencent, Inc.
 * Licensed under the MIT license
 */

.weui-flex {
  -webkit-box-align: center;
  -webkit-align-items: center;
  align-items: center;
}

.card-custom-dz {
  box-shadow: 0 0.5em 1em #eee;
}

.weui-cells {
  margin-top: 0;
  opacity: 0;
  -webkit-transform: translateY(-50%);
  transform: translateY(-50%);
  -webkit-transition: 0.3s;
  transition: 0.3s;
}

.weui-cells:after,
.weui-cells:before {
  display: none;
}

.weui-cells_show {
  opacity: 1;
  -webkit-transform: translateY(0);
  transform: translateY(0);
}

.weui-cell:before {
  right: 15px;
}

.kind-list__item {
  margin: 10px 0;
  background-color: #fff;
  border-radius: 2px;
  overflow: hidden;
}

.kind-list__item:first-child {
  margin-top: 0;
}

.kind-list__img {
  width: 30px;
  height: 30px;
}

.kind-list__item-hd {
  padding: 20px;
  -webkit-transition: opacity 0.3s;
  transition: opacity 0.3s;
}

.kind-list__item-hd_show {
  opacity: 0.4;
}

.kind-list__item-bd {
  height: 0;
  overflow: hidden;
}

.kind-list__item-bd_show {
  height: auto;
}

.custom-list-class-pd {
  padding: 10px 20px 10px 20px!important;
}

.custom-dz-list-image {
  height: 40px!important;
  width: 40px!important;
}
</style>
