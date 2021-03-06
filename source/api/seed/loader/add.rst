.. currentmodule:: Loader

add
======================================

| 添加/注册模块,和KISSY.use一起使用, 形成KISSY的模块加载体系


Module
-----------------------------------------------

  :mod:`Loader`

Methods
-----------------------------------------------

.. function:: KISSY.add
    :noindex:

    | void **KISSY.add** (name,fn)
    | 定义单个模块, 当你需要编写一个新的模块来满足你的需求时,请使用此方式.

    :param string name: 模块名称
    :param function fn: 模块定义函数, 若该模块的所有依赖项都已经载入完毕, 则 ``fn`` 立即执行
    
    
    范例: 一段典型的模块声明代码

    .. code-block:: javascript

        KISSY.add("yourmod",function(S){

            var D = S.DOM, E = S.Event
            //公共变量(常量)定义...

            /**
             * 类构造器
             */
            function YourMod(args){
                var self = this;
                //参数处理...
                //对象属性赋值...
                //初始化...
            }

            /**
             * 扩展原型方法
             */
            S.augment(YourMod, S.EventTarget, {
                /**
                 * 共有方法
                 */
                publicMethod:function(){
                    var self = this;
                },
                /**
                 * 私有方法
                 */
                _privateMethod:function(){
                    var self = this;
                }
            })

            //辅助方法...

            S.YourMod = YourMod;
            return YourMod;
        });

    
注册单个模块
--------------------------------------

.. function:: KISSY.add
    :noindex:

    | void **KISSY.add** (name,config)
    | 注册单个模块, 当你需要注册某个已有模块时,请使用此方式
    
    :param string name: 模块名称
    :param object config: 模块描述信息

    
    范例: 注册单个模块

    .. code-block:: javascript

        KISSY.add('yourmod',{
            fullpath:"http://xx.com/custommod.js",
            cssfullpath:"http://xx.com/custommod.css",
            requires:["depmod1","depmod2"]
        })


.. function:: KISSY.add
    :noindex:

    | void **KISSY.add** (config)
    | 注册多个模块, 当你需要注册多个已有模块时,请使用此方式
    
    :param object config: 模块描述信息
    
    范例: 注册多个模块

    .. code-block:: javascript

        KISSY.add({
            "custommod":{
                fullpath:"http://xx.com/custommod.js",
                cssfullpath:"http://xx.com/custommod.css",
                requires:["depmod1","depmod2"]
            },
            "custommod2":{
                fullpath:"http://xx.com/custommod2.js",
                requires:["depmod1","depmod2"]
            }
        });
 
 
    指明了模块 ``custommod`` 与 ``custommod2`` 的模块文件路径以及其依赖的模块名称,
    那么当 ``use`` 该模块时就会从 ``fullpath`` 中载入模块定义和其依赖模块的定义,
    以及从 ``cssfullpath`` 中载入模块的样式表
    
.. note::

    * ``fullpath`` 也可以直接是 css 文件, 这时该模块为 css 模块, 如果某个 js 模块依赖项配置了 css 模块, 则 js 模块的初始化会等待 css 模块对应的 css 文件完毕, 具体方法可见： `lifesinger 的探索 <http://lifesinger.wordpress.com/2011/05/02/seajs-css-support/>`_ .
        
    * 依赖的模块也要进行注册. 该函数用在模块注册文件中,kissy 1.2 使用包机制取代模块注册, 仍然兼容1.2以前模块注册方式.
    
    
    
    
    
    
    