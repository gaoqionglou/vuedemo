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
  </div>
</template>

<script>
import componentA from './components/a'
export default {
  components: {
    'component-a': componentA
  },
  data () {
    return {
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
      console.log('hanldeEmit --' + p)
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
.red-font {
  color: red;
}
.big-font {
  font-size: 20px;
}
.weight-font {
  font-weight: bolder;
}
</style>
