vue.js (IE8+，因为vue使用了IE8不能模拟的ECMAScript 5特性)
vue.js介绍
	vue.js是一套构建用户界面的渐进式框架。采用自底向上增量开发的设计，只关注视图层
	
	//声明式渲染
	Vue.js 的核心是一个允许采用简洁的模板语法来声明式的将数据渲染进 DOM 的系统
	<div id="app">{{message}}</div>
	new Vue({
		el:"#app",
		data:{
			message:"Hello Vue.js!"
		}
	})
	所有的元素都是响应式的；
	除了文本插值 还可以通过标签属性(指令)进行绑定
	<div id="app" v-bind:title="message">悬停查看</div>
		var app=new Vue({
			el:"#app",
			data:{
				message:"页面加载于"+new Date().toLocaleString()
			}
		})
	
	//条件与循环
	控制切换一个元素的显示											--*v-if*--
	<div id="app" v-if="message">悬停查看</div>
	不仅可以绑定DOM文本到数据 也可以绑定DOM结构到数据
	根据数组的数据来渲染一个项目列表						--*v-for*--
	<div id="app">
		<div v-for="(item,index) of/in message">		//要把v-for写在绑定的元素内 如果给#app循环会报错
	</div>
	<button></button>
	var app=new Vue({
		el:"#app",
		data:{
			message:[123,321,222]/[{name:"二狗"},{name:"二蛋"},{name:"二宝"}]
		}
	}) 
	以及可以向数组添加新的值
	document.getElementsByTagName("button")[0].onclick=()=>{app.message.push("Hello Vue.js!")}		//响应式的
	
	//处理用户输入
	为了让用户和应用进行绑定，可以使用v-on绑定一个事件监听器，通过它调用vue中的实例方法。		--*v-on*--
	<div id="app">
		<input :value="message" />
		<button @mousemove="change">我是按钮</button>
	</div>
	new Vue({  
		el:"#app",
		data:{
			message:"二宝二宝草鸡宝宝",
		},
		methods:{
			change:function(){
				this.message=this.message.split("").reverse().join("");
			}
			简写为
			change(){
				this.message=this.message.split("").reverse().join("");
			}
		}
	})
	vue还提供了v-model指令，能轻松实现表单输入和应用状态之间的双向绑定；
	<div id="app">
		<input v-model="message"/>
		<button @mousemove="change">{{message}}</button>
	</div>
	var app=new Vue({
		el:"#app",
		data:{
			message:"[123,321,222]"
		},
		methods:{
			change(){
				this.message=this.message.split("").reverse().join("");
			}
		}
	})

	//组件化应用构建
	组件系统是Vue的另一个重要概念，因为他是一种抽象，允许我们使用小型，独立和通常可复用的组件构成大型应用。
	在Vue中，一个组件本质上是拥有一个预定义选项的一个Vue实例，在Vue中组件注册很简单
	不循环
	Vue.component("ni-hao",{
		template:"<div>我是帅哥</div>"
	})
	循环
	<nihao v-for="x of message" :一个自定义名字="x"></nihao>
	Vue.component("nihao",{
		props:['一个自定义名字'],
		template:"<div>{{一个自定义名字}}</div>"
	})
	new Vue({
		el:"#app",
		data:{
			message:[123,321,222]
		}
	})
	一个自定义名字 类似变量 把循环的x与一个自定义名字进行绑定
	props类似一个接口 可以把需要调用的数据通过接口 接到组件里
	
		#与自定义元素的关系
			是web组件规范一部分 差别
				1.Vue 组件不需要任何补丁，并且在浏览器下表现一致。必要时，自定义组建也可以包裹在原生自定义元素内
				2.Vue 组件提供了纯自定义元素所不具备的一些重要功能，最突出的是跨组件数据流，自定义事件通信以及构建工具集成。
				



Vue 实例

	//创建一个Vue实例
	每个Vue 应用都是通过，vue函数创建一个新的实例开始
	var vm=new Vue({
		//选项
	})
	所有的Vue 组件都是Vue 实例，并且接受相同选项对象
	
	//数据与方法
	当一个Vue 实例被被创建时，它向Vue 的响应式系统中加入了其data对象中能找到的所有属性，当这些值改变时候，视图会产生响应
	<div id="change" :title="name">放上来查看</div>
	<button>点击</button>
	var datax=new Vue({
		el:"#change",
		data:{
			name:"fight!!!",
		}
	})
	document.getElementsByTagName("button")[0].onclick=()=>{console.log(datax.name);datax.name="fighting!"}
	
	值得注意的是 只有当 data中属性存在的时候 这些属性才会是响应式的
	如果新添加一个属性 datax.name1="1"; 是不会触发任何视图更新的
	解决方法为 把以后可能会需要的属性 设置为初始值 类似
	data:{
		newTodoText: '',
		visitCount: 0,
		hideCompletedTodos: false,
		todos: [],
		error: null
	}
	
	除了data属性，Vue 实例暴露了一些有用的实例属性和方法。他们都有前缀$，以便和用户自定义属性区分开
	例如
	console.log(datax.$data);		就和上方的 data属性相同 $el 为元素
	datax.$watch("name",function(newValue,oldvalue){
		window.close();					当点击上方按钮时候网页会关闭
	})
	
	//实例声明周期 
	每个Vue 实例在被创建之前都要经过一系列的初始化过程。例如需要设置数据监听，编译模版，挂在实例到DOM，在数据变化时更新DOM
	在这个过程中，会运行一些叫 生命周期钩子 的函数，给予用户在特定情况下添加自己的代码
	new Vue({
		el:"#change",
		data:{ 
			name:"fight!"
		},
		created:function(){
			this.name="fightingx!"						//钩子的this指向调用它的实例
		},
		updated:function(){
			console.log(111)
		}
	})
	document.getElementsByTagName("button")[0].onclick=()=>{console.log(datax.name);datax.name="fighting!"}
	点击后会console.log会为 	fightingx! 以及123  
	created 在创建时候改变了原来的name值 而 updated在点击 变更name值时候执行
	
	不要在选项属性或者回调上使用箭头函数，
	比如 created:()=>{}
	因为箭头函数是和父级上下文绑定在一起的；	他的指向是window 指向调用当前的环境

	//生命周期图示
	https://cn.vuejs.org/images/lifecycle.png
	



模板语法
	Vue.js使用了基于HTML的模板语法，允许开发者声明式的将DOM绑定至底层Vue实例的数据

	//插值
		//文本						--*v-once*--
		数据绑定最常见的就是用"Mustache"语法（双大括号）的文本插值
		<span>Message:{{msg}}</span>
		Mustache标签将会被替代为对应数据对象上msg属性的值，无论何时，绑定的数据对象上msg属性发生了改变，插值出的内容都会更新。
		
		通过使用v-once指令，执行一次性的插值，当数据改变时，插值处的内容不会更新。但是会影响当前节点所有数据
		<span v-once>Message:{{msg}}</span>
		
		//原始HTML			--*v-html*--
		双大括号会把数据解释为文本操作，而非HTML代码，为了输出真正的HTML，需要使用v-html指令
		<p>Using mustaches: {{ rawHtml }}</p>
		<p>Using v-html directive: <span v-html="rawHtml"></span></p>
		v-html 会让元素内部变成绑定的字符串格式 输入无法识别元素时会转换成自定义元素 前后标签不同 后标签会变成前标签 
		会忽略解析属性中的数据绑定 ⬅️
		站点上使用v-html是危险的，容易倒是XSS攻击，需要只对可信的内容进行v-html插值，绝不要对用户提供的内容进行插值
		在v-html内写字符串 无法编译

		//特性
		Mustache语法不能作用在html特性上，类似html属性等；应使用v-bind

        //使用Javascript表达式
        对于所有的数据绑定，vue.js都提供了完全的javscript表达式
        {{msg+1}}/{{ok?'yes':'no'}}/{{message.split("").reverse.join("")}}
        <div v-bind:id="'list-'+id"></div>
        每个绑定只能包含表达式

    //指令
    指令是带有v-前缀的特殊属性。指令属性的值预期是单个Javascript表达式（v-for除外）
    指令的作用是，当表达式的值改变时，将其产生的连带影响，响应式的作用于DOM
    <p v-if="msg">不知道能看到我不</p>

        //参数
        一些指令可以接受一些参数 在指令名称之后用冒号表示
        <a v-bind:href="url">超链接</a>
        <a v-on:click="func">点击有效果</a>

        //修饰符
        修饰符是以半角句号.指明的特殊后缀，用于指出一个指令应该以哪种特殊方式绑定
        例如  .prevent修饰符告诉v-on指令对于触发时间调用event.preventDefault()
        <from v-on:submit.prevent="onSubmit">

    //缩写
        //v-bind缩写
        <a v-bind:href="url"></a>
        <a :href="url"></a>
        //v-on缩写
        <a v-on:click="func"></a>
        <a @click="func"></a>




计算属性和观察者
    //计算属性
        //基础例子
        对于任何复杂属性，都应当使用计算属性
        <div id="message">
            <p v-html="change"></p>
            <p v-html="changex"></p>
        </div>
        new Vue({
            el:"#message",
            data:{
                change:"Hello Vue!"
            },
            computed:{
                changex:function(){
                    return this.change.split("").reverse().join("")
                }
            }
        })
        以上例子中的函数 始终依赖于 change 的值

        //计算属性缓存vs方法
        new Vue({
            el:"#message",
            data:{
                change:"hellox~",
            },
            methods:{
                changexx:function(){
                    return Date.now()
                }
            }
        })
        可以将同一函数定义为一个方法而不是一个计算属性。如果代码相同，返回的结果也是相同的。
        不同的是，计算属性是依赖缓存进行的，如果所依赖的发生改变时，才会重新计算
        methods里的事件会被事件执行（类似点击等） 而 computed不会被事件执行
            -------问题 如何验证computed是缓存执行的 通过 Date.now()-------
            
        methods为方法 调用时候需要用小括号调用 methods()
        而 computed 是属性 调用时候直接 .属性名 即可
         
		new Vue({
			el:"#appx",
			methods:{
				value1:function(){
					console.log("methods");
					return Date.now();
				},
				change(){
					console.log("methods"+this.value1());
					console.log("computed"+this.value2)
				}
			},
			computed:{
				value2:function(){
					console.log("computed");
					return Date.now();
				}
			}
		})

        //计算属性vs侦听属性
        	当有一些数据需要随着其他数据变动而变动时，最好使用 计算属性 而不是 wacth 回调
        	var vm=new Vue({
        	    el:"#appx",
        	    data:{
        	        name1:"nihao ",
        	        name2:"wohao",
        	        name3:"广州好迪",           //需要提前定义好要相应的改变的数据
        	    },
        	    watch:{
        	        name1:function(val){       //哪个为需要监听的变量，写在前方
        	            this.name3=val+this.name2   //需要改变的写在后方
        	        },
        	        name2:function(val){
        	            this.name3=val+this.name1
        	        }
        	    },
        	    methods:{
                    change(){
                        this.name1="奥迪双钻",
                        console.log(this.name3)
                    }
        	    }
        	})

        	var vm=new Vue({
        	    el:"#appx",
        	    data:{
        	        name1:"nihao ",
                    name2:"wohao",              //不需要提前命名name3
        	    },
        	    computed:{
        	        name3:function(){
        	            return this.name1+this.name2
        	        }
        	    },
        	    methods:{
                    change(){
                        this.name1="奥迪双钻",
                        console.log(this.name3)
                    }
                }
        	})
        	
        //计算属性的setter
        当给计算属性命名时候，会调用setter
        computed:{
            name3:{
                get:function(){
                    return this.name1+this.name2
                },
                set:function(val){
                    var names=val.split(" ");
                    this.name1=names[0];
                    this.name2=names[names.length-1]
                }
            }
        }
        当给name3命名时候 会调用set函数 name1和name2也会相对应的更新
        如果不命名会调用get函数 会返回新的name3

    //侦听器
    当在数据变化的时候，需要执行异步操作，或者执行开销较大的操作时，推荐这个方式
    使用 watch 选项允许我们执行异步操作 (访问一个 API)，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。
    这些都是计算属性无法做到的。




//Class与Style绑定
    //绑定HTML Class
    	//对象语法
	    可以传一个对象，以动态的切换class
	    .red{color:red;}
	    .heightx{height:200px}
	    <div id="appx" class="heightx" :class="{red:name1,heightx:name2}"></div>
	    new Vue({
	        el:"#appx",
	        data:{
	            name1:"香辣鸡脆骨",
	            name2:false,
	        }
	    })
	    --可以给class绑定对象，根据对象后的布尔值 判断是否添加class 不会和以前的calss冲突
	    
	    <div id="appx" :class="objx"></div>
	    new Vue({
	        el:"#appx",
	        data:{
	            objx:{
	                red:"香辣鸡脆骨",
	                heightx:false,
	            }
	        }
	    })
	    --可以直接给class直接绑定 对象名 对象内为需要展现的class 后为布尔值
	    
	    <div id="appx" :class="objx"></div>
	    new Vue({
	        el:"#appx",
	        data:{
	
	        },
	        computed:{
	            objx:function(){
	                return {
	                    red:true||false,
	                    heightx:true&&false
	                }
	            }
	        }
	    })
	    --也可以直接绑定computed计算属性 但需要返回一个对象
	    
		//数组语法
		<div :class="[name1,name2]">
		new Vue({
			el:"#appx",
			data:{
				name1:"liu",
				name2:"hongxiang",
			}
		})
		根据条件切换
		<div :class="[active?aaa:bbb,ccc]"></div>
		<div :class="[{active:aaa},bbb]"></div>
		
		//用在组件上
		当在一个自定义组件上使用class属性时，这些类将被添加到该组件的根元素上，这个元素上已经存在的类名不会被覆盖
		Vue.component("my-component",function(){
			template:"<p class='x1 x2'>nihao</p>"
		})
		在使用时候可以再添加一些类名
		<my-component class="z1 z2"></my-component>
		将被渲染为
		<p class="x1 x2 z1 z2"></p>
		对于带数据绑定的class同样使用，但是只可以在html结构里使用 不可以在template中使用
		<my-component :class="{bool:red}"></my-component>
	
	//绑定内联样式
		//对象语法
			绑定对象属性
			new Vue({
				el:"#appx",
				data:{
					datax:"red",
					width:"400px",
					height:500,
					border:"1px solid red",
				}
			})
			<p :style="{border:border,width:width,height:height+'px',color:datax}"></p>
			中间使用,逗号分隔

			或者		直接绑定对象
			
			new Vue({
				el:"#appx",
				data:{
					stylex:{
						color:"green",
						fontSize:"20px"
					}
				}
			})
			<div :style="stylex"></div>
			对象语法 通常结合返回对象的计算属性使用
			
		//数组语法
			new Vue({
				el:"#appx",
				data:{
					stylex:{
						color:"green",
						fontSize:"20px"
					},
			        stylez:{
			        	border:"1px solid black",
			        	fontWeight:"bolder"
			        }
				}
			})
			<div :style="[stylex,stylez]"></div>

		//自动添加前缀
		当v-bind:style使用需要添加浏览器前缀的属性时，如transform，Vue.js会自动侦测并添加	(-webkit- -moz- -ms-)
		
		//多重值
		2.3.0+
		可以为style绑定的属性提供一个包含多个值的数组，常用语提供多个带前缀的值
		<div :style="{display:['-webkit-box','-ms-flexbox','flex']}"></div>
		这样只会渲染数组中最后一个被浏览器支持的值。在本例中，如果浏览器支持不带浏览器前缀的flexbox，那么就只会渲染 display:flex




//条件渲染
	//v-if
	<p v-if="paiming">老大</p>	<p v-else>老二</p>
		//在template元素上使用v-if条件渲染分组
		<template v-if="paiming">
    		<p>大1</p>
    		<p>大2</p>
    	</template>
    	<template v-else>
    		<p>小1</p>
    		<p>小2</p>
    	</template>
    	
    	//v-else
    	v-else 元素必须紧跟在带 v-if 或者 v-else-if 的元素的后面，否则它将不会被识别。
    	
		//v-else-if
		v-else-if，顾名思义，充当 v-if 的“else-if 块”，可以连续使用
		v-else-if 也必须紧跟在带 v-if 或者 v-else-if 的元素之后。
		
		//使用key管理可复用元素
		Vue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。这么做除了使 Vue 变得非常快之外，还有其它一些好处。
		例如，如果你允许用户在不同的登录方式之间切换：
		<template v-if="paiming">
    		<input placeholder="文字">
    		<p>大2</p>
    	</template>
    	<template v-else>
			<input placeholder="数字">
			<p>小2</p>
    	</template>
    	切换时 input内容还在
    	解决方式 给复用元素 添加key值 <input placeholder="文字" key="da"> 和 <input placeholder="数字" key="er">
    	p仍然会被复用 因为没有添加key属性
    	
	//v-show
	另一个根据条件展示元素的选项是 v-show 指令 用法大致一样
		不同的是 v-show 会始终渲染并被保存在 DOM 元素中。v-show只是简单的切换 css的display 属性
		不支持 template 和 v-else 属性
		
	//v-show VS v-if
	v-if 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。
	v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。
	相比之下，v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。
	一般来说，v-if 有更高的切换开销，而 v-show 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 v-show 较好；
	如果在运行时条件很少改变，则使用 v-if 较好。
	
	当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级
	



//列表渲染
	//用v-for把一个数组对应为一组元素
	我们用 v-for 指令根据一组数组的选项列表进行渲染。v-for 指令需要使用 item in items 形式的特殊语法，items 是源数据数组并且 item 是数组元素迭代的别名。
	在 v-for 块中，我们拥有对父作用域属性的完全访问权限。v-for 还支持一个可选的第二个参数为当前项的索引。
	<ul>
		<li v-for="(item,index) in arr">{{fuji}}</li>
	</ul>
	第一个为值 第二个为下标
	
	//一个对象的v-for
	<ul>
		<li v-for="(valuexx,key,index) in arr">{{valuexx}}</li>
	</ul> 
	第一个为值 第二个为键 第三个为下标
	
	//key
	建议尽可能在使用 v-for 时提供 key，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。
	<div v-for="item in items" :key="item.id">
	  <!-- 内容 -->
	</div>
	
	//数组更新检测
		//变异方法
		Vue 包含一组观察数组的变异方法，所以它们也将会触发视图更新。这些方法如下：
		push()  pop()  shift()  unshift()  splice()  sort()  reverse()
		
		//替换数组
		变异方法，会改变被这些方法调用的原始数组。相比之下，也有非变异 (non-mutating method) 方法，例如：filter(), concat() 和 slice() 。
		这些不会改变原始数组，但总是返回一个新数组。当使用非变异方法时，可以用新数组替换旧数组：
		
		//注意事项
		由于 JavaScript 的限制，Vue 不能检测以下变动的数组：
		当你利用索引直接设置一个项时，例如：vm.items[indexOfItem] = newValue
		当你修改数组的长度时，例如：vm.items.length = newLength
		
			vm.items[indexOfItem] = newValue
			解决第一类问题
			Vue.set(example.items,indexOfItem,newValue)
			或
			example.items.splice(indexOfItem,1,newValue)
		
			vm.items.length = newLength
			解决第二类问题
			emample.items.splice(newLength);	newLength需小于当前数组长度 才可以截取 

	//对象更改检测注意事项
		由于 JavaScript 的限制，Vue 不能检测对象属性的添加或删除：
		var vm = new Vue({
		  data: {
		    a: 1
		  }
		})
		// vm.a现在是响应式的
		
		vm.b = 2
		// vm.b不是响应式的		数据里有 但不会更新到dom上
		
		对于已经创建的实例，Vue 不能动态添加根级别的响应式属性。但是，可以使用 Vue.set(object, key, value) 方法向嵌套对象添加响应式属性。
		Vue.set(vm.userProfile, 'age', 27);
		
	//显示过滤/排序结果
		有时，我们想要显示一个数组的过滤或排序副本，而不实际改变或重置原始数据。在这种情况下，可以创建返回过滤或排序数组的计算属性。
		<li v-for="n in evenNumbers">{{ n }}</li>
		data: {
		  numbers: [ 1, 2, 3, 4, 5 ]
		},
		computed: {
		  evenNumbers: function () {
		    return this.numbers.filter(function (number) {
		      return number % 2 === 0
		    })
		  }
		}
	
	//一段取值范围的v-for
		v-for 也可以取整数。在这种情况下，它将重复多次模板。
		<div>
		  <span v-for="n in 10">{{ n }} </span>
		</div>
		
	//v-for on a <template>
		类似于 v-if，你也可以利用带有 v-for 的 <template> 渲染多个元素。
		<ul>
		  	<template v-for="item in items">
			    <li>{{ item.msg }}</li>
			    <li class="divider"></li>
			</template>
		</ul>
	
	//v-for with v-if
		当它们处于同一节点，v-for 的优先级比 v-if 更高，这意味着 v-if 将分别重复运行于每个 v-for 循环中。
		当你想为仅有的一些项渲染节点时，这种优先级的机制会十分有用，如下：
		<div v-for='x of x' v-if='x.c'>{{x}}</div>
		var vm=new Vue({
		    el:"#appx",
		    data:{
		    	x:[{c:1},{c:2},{c:0},{c:4}]
		    },
		})
		只有 1 2 4显示
		
		而如果你的目的是有条件地跳过循环的执行，那么可以将 v-if 置于外层元素 (或 <template>)上。如：
		<div v-if='x.c'>
			<div v-for='x of x'>{{x}}</div> 
		</div>
		
	//一个组件的v-for
	在自定义组件里，你可以像任何普通元素一样用 v-for 。
	2.2.0+ 的版本里，当在组件中使用 v-for 时，key 现在是必须的。
	然而，任何数据都不会被自动传递到组件里，因为组件有自己独立的作用域。为了把迭代数据传递到组件里，我们要用 props ：
	
	完整demo
	<div id="appx">
		<div is="zhibiao" v-for="(x,index) in xx" :abc="x.name" :id="x.id" @xxx="xx.splice(index,1)"></div>
		<label for="">
			<button @click="change">添加</button>
			<input type="text" v-model="newName" placeholder="输入" />
		</label>
    </div>
	Vue.component("zhibiao",{
		template:'<div>{{abc}} <button @click="$emit(\'xxx\')">点我啊笨蛋</button></div>',
		props:["abc"],
	})
	new Vue({
	    el:"#appx",
	    data:{
	    	newName:"",
	    	xx:[{name:"大哥",id:1},{name:"二宝",id:2},{name:"三炮",id:3},],
	    	id:4,
	    },
	    methods:{
	    	change(){
	    		this.xx.push({
	    			id:this.id++,
	    			name:this.newName
	    		})
	    		this.newName="";
	    	}
	    }
	})
	



//事件处理
	//监听事件
		可以用 v-on 指令监听 DOM 事件，并在触发时运行一些 JavaScript 代码。
		<div id="example-1">
		  <button v-on:click="counter += 1">Add 1</button>
		  <p>The button above has been clicked {{ counter }} times.</p>
		</div>
		var example1 = new Vue({
		  el: '#example-1',
		  data: {
		    counter: 0
		  }
		}
	
	//事件处理方法
		然而许多事件处理逻辑会更为复杂，所以直接把 JavaScript 代码写在 v-on 指令中是不可行的。因此 v-on 还可以接收一个需要调用的方法名称。
		<div id="example-2">
		  <button v-on:click="greet">Greet</button>
		</div>
		
	//内联处理器中的方法
	<div id="example-3">
	  <button v-on:click="say('hi')">Say hi</button>
	  <button v-on:click="say('what')">Say what</button>
	</div>
	new Vue({
	  el: '#example-3',
	  methods: {
	    say: function (message) {
	      alert(message)
	    }
	  }
	})
	需要传入原生事件时候 传入$event
	
	//事件修饰符
	Vue.js 为 v-on 提供了事件修饰符。之前提过，修饰符是由点开头的指令后缀来表示的。
	.stop  .prevent  .capture  .self  .once
	<!-- 阻止单击事件继续传播 -->
	<a v-on:click.stop="doThis"></a>
	
	<!-- 提交事件不再重载页面 -->
	<form v-on:submit.prevent="onSubmit"></form>
	
	<!-- 修饰符可以串联 -->
	<a v-on:click.stop.prevent="doThat"></a>
	
	<!-- 只有修饰符 -->
	<form v-on:submit.prevent></form>
	
	<!-- 添加事件监听器时使用事件捕获模式 -->
	<!-- 即元素自身触发的事件先在此处处理，然后才交由内部元素进行处理 -->
	<div v-on:click.capture="doThis">...</div>
	
	<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
	<!-- 即事件不是从内部元素触发的 -->
	<div v-on:click.self="doThat">...</div>
	
		//2.14新增    .once事件将只执行一次 还能被用到自定义的组件事件上
		
	//按键修饰符
		<input v-on:keyup.13="submit">    //只有keycode为13时候才触发
		
		全部的按键别名
			.enter  .tab  .delete(捕获"删除"和"退格"键)  .esc  .space  .up  .down  .left  .right
			可以通过全集的config.keyCodes对象自定义按键修饰符别名
			Vue.config.keyCodes.f1=112
			
			//自动匹配按键修饰符
			你也可直接将 KeyboardEvent.key 暴露的任意有效按键名转换为 kebab-case 来作为修饰符：
			<input type="text" @keyup.page-down="change($event)">
			method:{
				change(xx){
					console.log(xx)					//在次可以查看暴露的key值
				}
			}
			处理函数只有在$event.key==="pageDown"时候被调用
			
	//系统修饰键
		可以用如下修饰符来实现仅在按下相应按键时才触发鼠标或键盘事件的监听器。
		.ctrl		.alt		.shift		.meta
		注意：在 Mac 系统键盘上，meta 对应 command 键 (⌘)。在 Windows 系统键盘 meta 对应 Windows 徽标键 (⊞)。
		在 Sun 操作系统键盘上，meta 对应实心宝石键 (◆)。在其他特定键盘上，尤其在 MIT 和 Lisp 机器的键盘、以及其后继产品，比如 Knight 键盘、space-cadet 键盘，meta 被标记为“META”。
		在 Symbolics 键盘上，meta 被标记为“META”或者“Meta”。(暂时备忘)
		
		修饰键和常规按键不同，在和keyup事件一起使用时候，事件触发时修饰键必须处于按下状态。
		
		.exact修饰符 允许控制由精准的系统修饰符组合触发的事件
		<!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
		<button @click.ctrl="onClick">A</button>
		
		<!-- 有且只有 Ctrl 被按下的时候才触发 -->
		<button @click.ctrl.exact="onCtrlClick">A</button>
		
		<!-- 没有任何系统修饰符被按下的时候才触发 -->
		<button @click.exact="onClick">A</button>
		
	//鼠标按键修饰符
		.left    .middle    .right		这些函数会限制处理函数仅响应特定的鼠标按钮
		



//表单输入绑定
	//基础用法
		可以使用v-model指令在表单<input><textarea>元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。
		v-model 会忽略所有表单元素的 value、checked、selected 特性的初始值而总是将 Vue 实例的数据作为数据来源。
		你应该通过 JavaScript 在组件的 data 选项中声明初始值。
		对于需要使用输入法 (如中文、日文、韩文等) 的语言，你会发现 v-model 不会在输入法组合文字过程中得到更新。如果你也想处理这个过程，请使用 input 事件。
		//文本
			<input v-model="message" placeholder="edit me">
			<p>Message is: {{ message }}</p>
		//多行文本
			<span>Multiline message is:</span>
			<p style="white-space: pre-line;">{{ message }}</p>
			<br>
			<textarea v-model="message" placeholder="add multiple lines"></textarea>
			在输入拼音时候不会更新，会自动换行
			
		//复选框
			单个复选框，绑定到布尔值：
			<input type="checkbox" id="checkbox" v-model="checked">
			<label for="checkbox">{{ checked }}</label>
			可以将多个复选框绑定到数组里
			
		//选择框 时将 v-model绑定到select上 给option设置value值
			选择框多选时 给select 设置 multiple布尔属性 设置值为空数组
			用 v-for 渲染的动态选项：
			<select v-model="selected">
			  <option v-for="option in options" v-bind:value="option.value">
			    {{ option.text }}
			  </option>
			</select>
			<span>Selected: {{ selected }}</span>
			new Vue({
			  el: '...',
			  data: {
			    selected: 'A',
			    options: [
			      { text: 'One', value: 'A' },
			      { text: 'Two', value: 'B' },
			      { text: 'Three', value: 'C' }
			    ]
			  }
			})
			
	//值绑定
		//对于单选按钮，复选框及选择框的选项，v-model绑定的值通常是静态字符串(对于复选框，也可以是布尔值)
			<!-- 当选中时，`picked` 为字符串 "a" -->
			<input type="radio" v-model="picked" value="a">
			
			<!-- `toggle` 为 true 或 false -->
			<input type="checkbox" v-model="toggle">
			
			<!-- 当选中时，`selected` 为字符串 "abc" -->
			<select v-model="selected">
			  <option value="abc">ABC</option>
			</select>
			但是有时我们可能想把值绑定到 Vue 实例的一个动态属性上，这时可以用 v-bind 实现，并且这个属性的值可以不是字符串。
		
		//复选框
			<input type="checkbox" v-model="xxx" true-value="你好" false-value="不好" />
			<input type="text" :value="xxx" />
			
		//单选框
			<input type="radio" v-model="pick" v-bind:value="a">
			// 当选中时
			vm.pick === vm.a
			
		//选择框的选项
			<select v-model="selected">
			    <!-- 内联对象字面量 -->
			  <option v-bind:value="{ number: 123 }">123</option>
			</select>
			vm.selected.number==123
			
	//修饰符
		v-model.lazy				
		默认情况下为及时响应式，加lazy后 使每次的input事件转变为change事件或者点击enter也可以进行更新
		
		v-model.number
		将用户输入的值转变为数值类型，默认情况下输入数字为字符串类型，.number会转化为数值，并且如果后面为字符串会只截取前面为数字的部分
		
		v-mode.trim
		将会自动过滤首尾空白字符
		



//组件
组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素，Vue.js 的编译器为它添加特殊功能。
在有些情况下，组件也可以表现为用 is 特性进行了扩展的原生 HTML 元素。
	
	//使用组件
		//全局注册
			创建vue实例
			new Vue({
				el:"#appx",
			})
			注册全局组件
			Vue.component("my-component",{
				template:"<div>123</div>"
			})
			
			要确保注册全局组件在 创建Vue实例之前 Vue实例对象才可以继承
			
		//局部注册
			可以通过Vue实例/组件的实例选项components注册仅在其作用域中可用的组件
			new Vue({
				components:{
					"zuJianMing":{
						template:"<div>123</div>"
					}
				}
			})
			这种封装也适用于其它可注册的 Vue 功能，比如指令。

		//DOM模版解析注意事项
			当使用 DOM 作为模板时 (例如，使用 el 选项来把 Vue 实例挂载到一个已有内容的元素上)，你会受到 HTML 本身的一些限制，
			因为 Vue 只有在浏览器解析、规范化模板之后才能获取其内容。
			尤其要注意，像 <ul>、<ol>、<table>、<select> 这样的元素里允许包含的元素有限制，而另一些像 <option> 这样的元素只能出现在某些特定元素的内部。
			
			<table>
			  <my-row>...</my-row>			//会解析无效 应当使用is绑定到元素上
			</table>
			应当注意，如果使用来自以下来源之一的字符串模板，则没有这些限制：
				<script type="text/x-template">
				JavaScript 内联模板字符串
				.vue 组件
				因此，请尽可能使用字符串模板。
				
		//data必须是函数
			data为component/components里面的属性 
			如果不为函数则会报错	
			new Vue({
				el:"#appx",
				components:{
					"niHao":{
						template:"<div>{{xx}}</div>",
						data:function(){
							return {
								xx:"1231"
							}
						}
					}
				}
			})
			
		//组件组合
			父子组件的关系可以总结为 prop向下传递，事件向上传递
			父组件通过prop给子组件下发数据，子组件通过事件给父组件下发数据。
			
	//Prop
		//使用prop传递数据
			<ni-hao :xx="xxz"></ni-hao>			使用组件时候 让数据绑定到预设的props的属性上
			new Vue({
			    el:"#appx",
			    data:{
			    	xxz:"123",
			    },
			    components:{
			    	"niHao":{
			    		template:"<div>{{xx}}</div>",
			    		props:["xx"]
			    	}
			    }
			})
			
		//camelCase vs kebab-case
			HTML特性是不区分大小写的 如果使用的不是字符串模版("<div>字符串模版</div>")时，camleCase的prop需要转化为相应的camle-case
			使用字符串模版时，则没有这些限制
			
		//动态Prop
			<div>
			  <input v-model="parentMsg">
			  <br>
			  <child :my-message="parentMsg"></child>
			</div>
			使用v-bind绑定响应式数据
			也可以对 对象进行传递
			
		//字面量语法 vs 动态语法
			如果想传递数字1
			<ni-hao propx="1"><ni-hao>			//传递字符串1
			<ni-hao :propx="1"><ni-hao>			//如果想传递一个真正的 JavaScript 数值，则需要使用 v-bind，从而让它的值被当作 JavaScript 表达式计算
			
		//单项数据流
			Prop 是单向绑定的：当父组件的属性变化时，将传导给子组件，但是反过来不会。这是为了防止子组件无意间修改了父组件的状态，来避免应用的数据流变得难以理解。
			另外，每次父组件更新时，子组件的所有 prop 都会更新为最新值。
			在两种情况下，我们很容易忍不住想去修改 prop 中数据：
			Prop 作为初始值传入后，子组件想把它当作局部数据来用；
				props: ['initialCounter'],
				data: function () {
				  return { counter: this.initialCounter }
				}
			Prop 作为原始数据传入，由子组件处理成其它数据输出。
				props: ['size'],
				computed: {
				  normalizedSize: function () {
				    return this.size.trim().toLowerCase()
				  }
				}
			注意javascript中的对象和数组是 引用传递，指向了内存的同一地址，如果prop是一个对象或数组，在子组件内部改变它会影响父组件的状态。
			
		//Prop验证
			我们可以为组件的 prop 指定验证规则。如果传入的数据不符合要求，Vue 会发出警告。
			Vue.component('example', {
			  props: {
			    // 基础类型检测 (`null` 指允许任何类型)
			    propA: Number,
			    // 可能是多种类型
			    propB: [String, Number],
			    // 必传且是字符串
			    propC: {
			      type: String,
			      required: true				required//必须 true
			    },
			    // 数值且有默认值
			    propD: {
			      type: Number,
			      default: 100
			    },
			    // 数组/对象的默认值应当由一个工厂函数返回
			    propE: {
			      type: Object,
			      default: function () {
			        return { message: 'hello' }
			      }
			    },
			    // 自定义验证函数
			    propF: {
			      validator: function (value) {
			        return value > 10
			      }
			    }
			  }
			})  
			type 可以是下面原生构造器：String	Number	Boolean	Function	Object	 Array	Symbol
			type 也可以是一个自定义构造器函数，使用 instanceof 检测。
			当 prop 验证失败，Vue 会抛出警告 (如果使用的是开发版本)。注意 prop 会在组件实例创建之前进行校验，
			所以在 default 或 validator 函数里，诸如 data、computed 或 methods 等实例属性还无法使用。
			
	//非prop特性
		例如，假设我们使用了第三方组件 bs-date-input，它包含一个 Bootstrap 插件，该插件需要在 input 上添加 data-3d-date-picker 这个特性。这时可以把特性直接添加到组件上 (不需要事先定义 prop)：
		<bs-date-input data-3d-date-picker="true"></bs-date-input>
		添加属性 data-3d-date-picker="true" 之后，它会被自动添加到 bs-date-input 的根元素上。
		
		//替换/合并现有的特性
			ni-hao的模板	<div class="a">123</div>
			<ni-hao class="b"></ni-hao>	
			class 和 style 特性会更聪明一些，这两个特性的值都会做合并 (merge) 操作
			
	//自定义事件
		子组件和父组件通信 通过自定义事件
		子组件通过绑定一个事件 里面传入 $emit("父组件监听事件名",参数)		父组件监听里面事件 并执行相应函数
		Vue.component("niHao",{
			data:function(){
				return {
					x:0
				}
			},
			template:"<div @click='dianji'>{{x}}</div>",
			methods:{
				dianji(){
					this.x+=1;
					this.emit("chuandi",this.x);
				}
			}
		})
		<ni-hao @chuandi='change'></ni-hao>
		new Vue({
			el:"#appx",
			data:{
				xx:0,
			},
			methods:{
				change(value){
					alert(value)
				}
			}
		})
		子组件已经和它外部完全解耦了。它所做的只是报告自己的内部事件，因为父组件可能会关心这些事件。
