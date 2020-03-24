<template>
  <div id="app">
    <h1>Vue-Demo</h1>
     <component-a></component-a>
     <h4>vtext/vhtml</h4>
     <p v-text="vtext"></p>
     <p v-html="vhtml" :class="['weight-font',className]"></p>
     <br>
     <h4>v-for数组</h4>
     <ul>
       <li v-for="(item, index) in vforDataArray" :key="index">{{index+1}} : {{item}}</li>
     </ul>
     <br>
     <h4>v-for对象</h4>
      <ul>
       <li v-for="(value, key) in vofrDataObj" :key="key">{{key}} : {{value}} </li>
     </ul>
     <br>
     <h4>v-for对象数组</h4>
      <ul>
       <li v-for="(item, index) in vforDataObjList" :key="index">{{index+1}} : {{item.type}} / {{item.name}} / {{item.price}}</li>
     </ul>
     <br>
     <h4>v-model 输入框</h4>
     <input type="text" v-model="inputValue"/> 输出： {{inputValue}}
     <h4>v-model checkbox</h4>
     <input type="checkbox" v-model="vModelBox" value="奔驰"/>
     <input type="checkbox" v-model="vModelBox" value="宝马"/>
     <input type="checkbox" v-model="vModelBox" value="法拉利"/>
     输出： {{vModelBox}}<br>
      <h4>v-model 下拉菜单</h4>
       <select v-model="myselection">
         <option value="国语">国语</option>
         <option value="法语">法语</option>
         <option value="罗马语">罗马语</option>
       </select>
       <br>
       <select v-model="myselection">
         <option v-for="(item, index) in selectOption" :key="index" :value="item.value">{{item.text}}</option>
       </select>
       输出：{{myselection}}
        <h4>自定义方法 使用emit()</h4>
        <component-a @myevent="hanldeEmit">Emit</component-a>
        <br>
        <h4>计算属性</h4>
        <input v-model="myValue" type="text"/> 计算属性{{myValueWithoutNumber}}
        通过方法获取{{getMyValWithoutNumber()}}
        <br>
        <h4> watch </h4>
        <input type="text" v-model="watchValue"/>
        <ul>
          <li v-for="(item,index) in watchList" :key="index">{{item.name}} = {{item.price}}</li>
        </ul>
        <button @click="changeList">changeList</button>
        <br>
        <h4> 组件参数传递 </h4>
        静态值：<br>
        <component-a data="the data from App.vue"></component-a>
        动态值：<br>
        <input type="text" v-model="myValue"/>
        <component-a :my-value="myValue">
        <p slot="header">xxx header</p>
        <p slot="footer">xxx footer</p>
        </component-a>
        <br>
        <h4>动态组件</h4>
        <button @click="changeView">changeView</button>
        <p :is="currentView"></p>
        <h4>css过渡效果</h4>
        <div class="ab">
          <transition name="fade">
          <p v-show="show">I am show</p>
          </transition>
          <transition name="my-trans" mode="out-in">
          <p v-if="show" key="1">I am show</p>
          <p key="2" v-else>not in show</p>
          </transition>
           <button @click="show = !show">Toggle</button>
          <transition name="fade" mode="out-in">
          <p :is="currentView">w</p>
          </transition>
           <button @click="toggleComponent">Toggle组件</button>
        </div>
        <h4>JS过渡效果</h4>
        <div>
          <transition
          @before-enter="beforeEnter"
          @enter="enter"
          @leave="leave"
          :css="false">
          <p class="animate-p" v-show="show">showing content</p>
          </transition>
        </div>
        <h4>自定义指令</h4>
        <p v-color="'red'">自定义指令1</p>
        <p v-customcolor="'green'"> 自定义指令2</p>
        <input type="text" v-focus>
  </div>
</template>

<script>
import componentA from './components/a'
import Vue from 'vue'
import componentB from './components/b'
import componentC from './components/c'
import HelloWorld from './components/HelloWorld'
export default {
  components: {
    'component-a': componentA,
    'component-b': componentB,
    'component-c': componentC,
    HelloWorld
  },
  directives: {
    color: function (el, binding) {
      el.style.color = binding.value
    },
    customcolor: function (el, binding) {
      el.style.color = binding.value
    },
    focus: {
      inserted (el, binding) {
        el.focus()
      }
    }
  },
  data () {
    return {
      show: true,
      currentView: 'component-a',
      watchValue: '',
      watchList: [{
        name: '苹果',
        price: 10
      },
      {
        name: '香蕉',
        price: 15
      }],
      myValue: '',
      myselection: null,
      selectOption: [{
        text: '苹果',
        value: 0
      },
      {
        text: '香蕉',
        value: 1
      }],
      inputValue: '',
      vModelBox: [],
      vtext: '测试vtext',
      vhtml: '<span>test v-html</span>',
      classStr: 'red-font',
      className: {
        'red-font': true,
        'big-font': true
      },
      vofrDataObj: {
        type: 'car',
        name: 'SUV-BXX',
        price: '$20K'
      },
      vforDataArray: ['American', 'Russia', 'China'],
      vforDataObjList: [ {
        type: 'car',
        name: 'SUV-BXX',
        price: '$20K'
      }, {
        type: 'fruit',
        name: 'apple',
        price: '$10K'
      }, {
        type: 'cosmetic',
        name: 'makeup stuff',
        price: '$30K'
      }]
    }
  },
  methods: {
    hanldeEmit (p) {
      var a = this.$http.get('https://www.baidu.com')
      console.log('hanldeEmit --' + a)
    },
    getMyValWithoutNumber () {
      return this.myValue.replace(/\d/g, '')
    },
    changeList () {
      Vue.set(this.watchList, 1, {
        name: 'stawberry',
        price: 88
      })
      // this.tellUser()
    },
    tellUser () {
      alert('list changed')
    },
    changeView () {
      this.currentView = 'HelloWorld'
    },
    toggleComponent () {
      if (this.currentView === 'component-c') {
        this.currentView = 'component-b'
      } else {
        this.currentView = 'component-c'
      }
    },
    beforeEnter: function (el) {
      $(el).css({
        left: '-500px',
        opacity: 0
      })
    },
    enter: function (el, done) {
      $(el).animate({
        left: 0,
        opacity: 1
      }, {
        duration: 1500,
        complete: done
      })
    },
    leave: function (el, done) {
      $(el).animate({
        left: '500px',
        opacity: 0
      }, {
        duration: 1500,
        complete: done
      })
    }
  },
  watch: {
    watchValue: function (val, oldVal) {
      console.log(val + '---' + oldVal)
    },
    watchList: function () {
      alert('[watch] list change')
    }
  },
  computed: {
    myValueWithoutNumber () {
      return this.myValue.replace(/\d/g, '')
    }
  }
}
</script>

<style>
a {
  color: cornflowerblue;
}
html {
  height: 100%;
}
body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.red-font {
  color: red;
}
.big-font {
  font-size: 20px;
}
.weight-font {
  font-weight: bolder;
}
.fade-enter-active, .fade-leave-active{
  transition: opacity .5s ease-out;
}
.fade-enter, .fade-leave-active{
  opacity: 0;
}
.my-trans-enter-active, .my-trans-leave-active {
  transition: all .5s ease-out;
}
.my-trans-enter {
  transform: translateX(-500px);
  opacity: 0;
}
.my-trans-leave-active{
  transform: translateX(500px);
  opacity: 0;
}
.animate-p {
  position: absolute;
  top: 0;
  left: 0;
}
</style>
