<template>
  <div class="home">
    <!-- <h1>上课点名</h1> -->
    <!-- <div class="box">
      <div
        class="k"
        :class="{active:selIndex==i}"
        v-for="(k, i) in arr"
        :key="i"
        @click="selFun(i)"
      >{{i+1}} : {{k.txt}}</div>
    </div>
    <div class="show-box">{{sel}}</div>-->

    <!-- <h1>上课点名</h1>
    <div class="box">
      <div
        class="k"
        :class="{active:data.selIndex==i}"
        v-for="(k, i) in data.arr"
        :key="i"
        @click="data.selFun(i)"
      >{{i+1}} : {{k.txt}}</div>
    </div>
    <div class="show-box">{{data.sel}}</div>-->

    <h1>上课点名</h1>
    <div class="box">
      <div
        class="k"
        :class="{active:selIndex==i}"
        v-for="(k, i) in arr"
        :key="i"
        @click="selFun(i)"
      >{{i+1}} : {{k.txt}}</div>
    </div>
    <div class="show-box">{{sel}}</div>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
  ref,
  reactive,
  toRefs,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted,
  onActivated,
  onDeactivated,
} from "vue";

export default defineComponent({
  name: "Home",
  components: {
    // HelloWorld,
  },
  // ### 一. setup 生命周期的钩子函数
  /*
    在vue3中，直接全部写在setup函数中就行，首先先来说说这个setup是什么，这个其实就是个生命周期的钩子函数，
    相对于vue2，他就等于vue2的beforeCreate和create两个生命周期函数，
    在vue3中他不仅仅是一生命周期函数，
    同时我们需要通过这个函数来定义vue2中的data,methods,watch,computed属性，所以我们上面说到的定义的两个属性和方法都定义到了其中，
    但是最后都需要return回去，并且写法有很大的一点不同是，我们对其赋值或者取值的时候必须是通过**.value 的写法去拿或者取，
    最终我们不管他是属性还是方法都需要return**回去之后才能使用
  */

  /*
    总结:
    setup和ref做一个总结：

    1.setup函数其实是一个生命周期钩子，它对应的其实就是Vue2中的beforeCreate和create，
      并且他是vue3的composition API的入口函数。

    2.在vue3中我们通过这个函数来定义vue2中的data,methods,watch,computed属性

    3.setup函数必须有返回值，必须返回一个对象，对象里包含所有在template模板中需要使用到的属性（包含data,methods等）

    4.在setup里面通过ref生命的响应式数据，去取值或者赋值的时候必须通过**.value的方法去拿，
      但是template却不需要使用.value**
    
    5.ref也可以调用原生dom

    6.setup接收第一个参数是props，用于接收props，也就是定义在组件上的属性（同vue2),
      但是接收的props必须先在props属性中定义，否则是不会被接收到的
    
    7.setup接收的第二个参数是context,在js里面这个形参代表了上下文，它暴露组件的 property，
      他就是一个普通的javaScript对象，在这里面我们可以取到attrs,** slots**,** emit**，等属性，
      所以可以干嘛我想各位都知道了。
  */

  /*
    注意:
    props是响应式的数据，你不能使用 ES6 解构，因为它会消除 prop 的响应性。
    我们可以尝试一下将 props 进行 ES6 解构，会发现控制台报警了，
    所以，要结构props需要用到setup 函数中的 toRefs 来安全地完成此操作，后面再来说这个函数。
  */

  // setup() {
  //   /*
  //     在vue3中，我们需要通过ref关键字进行包括，这样的操作才能将它定义为一个响应式的数据，
  //     ref函数是一个把普通变量变成Proxy响应式变量的函数
  //     ref的另一个用法可以调用原生的DOM
  //   */
  //   const arr = ref([
  //     {
  //       txt: "我是1",
  //     },
  //     {
  //       txt: "我是2",
  //     },
  //     {
  //       txt: "我是3",
  //     },
  //   ]);

  //   const sel = ref("");
  //   sel.value = arr.value[0].txt;

  //   const selIndex = ref(0);

  //   const selFun = (index: number) => {
  //     console.log("index", index);
  //     console.log("arr", arr);
  //     console.log("arr", arr.value[index]);
  //     console.log("arr", arr.value[index].txt);
  //     // selIndex = ref(index);
  //     // sel.value = arr.value[index];
  //     sel.value = arr.value[index].txt;
  //   };

  //   return { arr, sel, selFun, selIndex };
  // },

  /*
  reactive:

  1.不再使用ref对属性进行申明响应式，而是和类似vue2的写法，我只需要定义一个data对象即可，
    想要的属性都放在data，最后统一返回data即可。

  2.不再使用**.value的方式而改用data.**这样的方式，更方便自己理解，
    当然同理，template也需要加上，对我个人而言，，我觉得这种的写法更为清晰，更好理解。

  3.不需要再return一堆东西了，只需要return一个对象就可以了，写法更加简洁。
  */

  // setup() {
  //   const data = reactive({
  //     arr: [
  //       {
  //         txt: "张三",
  //       },
  //       {
  //         txt: "李四",
  //       },
  //       {
  //         txt: "王五",
  //       },
  //     ],
  //     sel: "",
  //     selIndex: 0,
  //     selFun: (index: number) => {
  //       console.log("index", index);
  //       console.log("data.arr", data.arr);
  //       data.sel = data.arr[index].txt;
  //       data.selIndex = index;
  //     },
  //   });
  //   data.sel = data.arr[0].txt;
  //   //  {...data} 这样会失去 数据响应
  //   return { data };
  // },

  // toRefs()函数对reavtive()函数解构返回 --> 这种方式最合适,跟vue2.x很像的写法
  // 就是data,methods
  // setup() :开始创建组件之前，在beforeCreate和created之前执行。创建的是data和method
  // setup() {
  //   console.log("生命周期 setup");
  //   const data = reactive({
  //     arr: [
  //       {
  //         txt: "张三",
  //       },
  //       {
  //         txt: "李四",
  //       },
  //       {
  //         txt: "王五",
  //       },
  //     ],
  //     sel: "",
  //     selIndex: 0,
  //     selFun: (index: number) => {
  //       console.log("index", index);
  //       console.log("data.arr", data.arr);
  //       data.sel = data.arr[index].txt;
  //       data.selIndex = index;
  //     },
  //   });
  //   data.sel = data.arr[0].txt;
  //   const resData = toRefs(data);
  //   return { ...resData };
  // },

  // ### 二. vue2   vue3   vue2和3的部分差异比较
  /*
  
  vue2  	          vue3  	            vue2和3的部分差异比较
  beforeCreate	    setup	              setup() :开始创建组件之前，在beforeCreate和created之前执行。创建的是data和method
  created	          setup
  beforeMount	      onBeforeMount	      组件挂载到节点上之前执行的函数
  mounted           onMounted           组件挂载完成后执行的函数。
  beforeUpdate      onBeforeUpdate      组件更新之前执行的函数。
  updated           onUpdated           组件更新完成之后执行的函数。
  beforeDestroy     onBeforeUnmount     卸载之前执行的函数。相比改名了
  destroyed         onUnmounted         卸载之后执行的函数。
  activated         onActivated         被包含在中的组件，会多出两个生命周期钩子函数。被激活时执行。
  deactivated       onDeactivated       比如从 A 组件，切换到 B 组件，A 组件消失时执行。
  errorCaptured     onErrorCaptured     当捕获一个来自子孙组件的异常时激活钩子函数。
                    onRenderTracked	    vue3新增的周期用于开发调试使用的
                    onRenderTriggered	  vue3新增的周期用于开发调试使用的
  */

  //  setup() :开始创建组件之前，在beforeCreate和created之前执行。创建的是data和method
  setup() {
    console.log("生命周期setup");
    // 组件挂载到节点上之前执行的函数

    const data = reactive({
      arr: [
        {
          txt: "张三",
        },
        {
          txt: "李四",
        },
        {
          txt: "王五",
        },
      ],
      sel: "",
      selIndex: 0,
      selFun: (index: number) => {
        console.log("index", index);
        console.log("data.arr", data.arr);
        data.sel = data.arr[index].txt;
        data.selIndex = index;
      },
    });
    data.sel = data.arr[0].txt;
    const resData = toRefs(data);

    // ---------- 生命周期 开始 ----------
    onBeforeMount(() => {
      console.log("生命周期onBeforeMount1");
    });

    // 组件挂载完成后执行的函数。
    onMounted(() => {
      console.log("生命周期onMounted2");
    });
    // 组件更新之前执行的函数。
    onBeforeUpdate(() => {
      console.log("生命周期onBeforeUpdate3");
    });
    // 组件更新完成之后执行的函数。
    onUpdated(() => {
      console.log("生命周期onUpdated4");
    });
    // 卸载之前执行的函数。相比改名了
    onBeforeUnmount(() => {
      console.log("生命周期onBeforeUnmount5");
    });
    // 卸载之后执行的函数。
    onUnmounted(() => {
      console.log("生命周期onUnmounted6");
    });
    // 被包含在中的组件，会多出两个生命周期钩子函数。被激活时执行。
    onActivated(() => {
      console.log("生命周期onActivated7");
    });
    // 比如从 A 组件，切换到 B 组件，A 组件消失时执行。
    onDeactivated(() => {
      console.log("生命周期onDeactivated8");
    });
    // ---------- 生命周期 结束 ----------

    return { ...resData };
  },
});
</script>

<style lang="scss" scoped>
.home {
  .box {
    display: flex;
    border-bottom: 1px solid #666;
    .k {
      width: 200px;
      height: 50px;
      line-height: 50px;
      text-align: center;
      cursor: pointer;
      &.active {
        color: white;
        background-color: red;
      }
    }
  }
  .show-box {
    margin-top: 20px;
  }
}
</style>
