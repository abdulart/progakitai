<template>
  <div class="page">
    <div class="page__hd">
      <div class="page__title">Apply to the University</div>
      <div class="page__desc">Nice description here</div>
    </div>

    <div class="page__bd">

      <div class="weui-cells__title">選擇城市</div>
      <div class="weui-cells weui-cells_after-title">
        <div class="weui-cell weui-cell_select">
          <div class="weui-cell__bd">
            <picker @change="bindCityChange" :range="cities">
              <div class="weui-select">{{cities[cityIndex]}}</div>
            </picker>
          </div>
        </div>
      </div>

      <div class="weui-cells__title">選擇大學</div>
      <div class="weui-cells weui-cells_after-title">
        <div class="weui-cell weui-cell_select">
          <div class="weui-cell__bd">
            <picker @change="bindUniversityChange" :range="universities[cities[cityIndex]]">
              <div class="weui-select">{{universities[cities[cityIndex]][universityIndex]}}</div>
            </picker>
          </div>
        </div>
      </div>

      <div class="weui-cells__title">你的評論</div>
      <div class="weui-cells weui-cells_after-title">
        <div class="weui-cell">
          <div class="weui-cell__bd">
            <textarea class placeholder="请输入文本" style="height: 3.3em" />
            <div class="weui-textarea-counter">0/200</div>
          </div>
        </div>
      </div>

      <div class="weui-btn-area">
        <button class="weui-btn" type="primary" @click="showTopTipsFun">确定</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showTopTips: false,
      time: '09:01',
      date: '2015-09-01',
      countryCodes: ["+86", "+80", "+84", "+87"],
      countryCodesIndex: 0,
      countries: ["中国", "美国", "英国"],
      countryIndex: 0,
      accounts: ["微信号", "QQ", "Email"],

      // Cities from DB
      cities: ['Moscow', 'SPB', 'Kazan'],
      cityIndex: 0,

      // Universities from DB
      universities: {
        'Moscow': ['MSU', 'Bauman', 'MFTI'],
        'SPB': ['SPBGU', 'SPBTU'],
        'Kazan': ['KGU', 'KMGU']
      },
      universityIndex: 0,

      accountsIndex: 0,

      radioItems: [
        { name: 'cell standard', value: '0' },
        { name: 'cell standard', value: '1', checked: true }
      ],
      checkboxItems: [
        { name: 'standard is dealt for u.', value: '0', checked: true },
        { name: 'standard is dealicient for u.', value: '1', checked: false }
      ],

      isAgree: false
    }
  },
  methods: {
    bindUniversityChange(e) {
      this.universityIndex = e.mp.detail.value;
    },

    bindCityChange(e) {
      this.universityIndex = 0;
      this.cityIndex = e.mp.detail.value;
    },










    checkboxChange(e) {
      console.log('checkbox发生change事件，携带value值为：' + e.mp.detail.value);
      var checkboxItems = this.checkboxItems;
      var values = e.mp.detail.value;
      for (var i = 0, lenI = checkboxItems.length; i < lenI; ++i) {
        checkboxItems[i].checked = false;

        for (var j = 0, lenJ = values.length; j < lenJ; ++j) {
          if (checkboxItems[i].value === values[j]) {
            checkboxItems[i].checked = true;
            break;
          }
        }
      }
      this.checkboxItems = checkboxItems;
    },
    radioChange(e) {
      console.log('radio发生change事件，携带value值为：' + e.mp.detail.value);
      let radioItems = this.radioItems;
      for (let i = 0; i < radioItems.length; ++i) {
        radioItems[i].checked = radioItems[i].value === e.mp.detail.value;
      }
      this.radioItems = radioItems;
    },
    switchChange(e) {
      console.log("switch发生change事件，携带value值为：" + e.mp.detail.value);
    },
    bindDateChange(e) {
      this.date = e.mp.detail.value;
      console.log(e.mp.detail.value);
    },
    bindTimeChange(e) {
      this.time = e.mp.detail.value;
      console.log(e.mp.detail.value);
    },
    showTopTipsFun() {
      this.showTopTips = true;
      setTimeout(() => {
        this.showTopTips = false;
      }, 2000)
    },

    bindCountryChange(e) {
      this.countryIndex = e.mp.detail.value;
    },
    bindAccountChange(e) {
      this.accountsIndex = e.mp.detail.value;
    },
    bindCountryCodeChange(e) {
      this.countryCodesIndex = e.mp.detail.value;
    },
    bindAgreeChange(e) {
      this.isAgree = !this.isAgree;
    }
  }
}
</script>

<style>
</style>
