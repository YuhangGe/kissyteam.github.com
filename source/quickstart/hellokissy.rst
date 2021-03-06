.. _quickstart-hellokissy:


Hello KISSY
===============================================

在前一小节的示例中, 用到了 KISSY 常用的 ``DOM``, ``Event``, ``Anim`` 等功能.

完整代码如下:

.. code-block:: javascript
   :linenos:
   
    KISSY.ready(function(S){
        var DOM = S.DOM, Event = S.Event,
            btn = DOM.get('#demo-btn');

        Event.on(btn, 'click', function() {
            DOM.attr(btn, 'disabled', true);

            S.Anim('#demo-img', 'left: 400px; opacity: 0', 2, 'easeOut', function() {
                S.Anim('#demo-txt',
                       'left: 0; opacity: 1; fontSize: 28px',
                       2, 'bounceOut').run();
            }).run();
        });
    });


这个例子中, 
    #. :func:`KISSY.ready() <Web.KISSY.ready>` 指在 DOM 加载完毕之后执行代码. 就像 jQuery 中的 ``$(document).ready()``.
    #. :mod:`DOM`, KISSY 的 DOM 模块 [1]_ , 提供常用 DOM 操作, 如元素选择/遍历, 样式的获取/修改等等.
    #. :mod:`Event`, KISSY 的 Event 模块 [2]_ , 提供事件处理功能, 如事件添加/删除, ``mouseenter/mouseleave`` 事件的支持等.
    #. :func:`DOM.get(selector) <DOM.get>`, 根据给出的 ``selector`` 获取符合条件的 **第一个节点**; 另外还有一个类似的方法叫做 :func:`DOM.query(selector) <DOM.query>` , 与前者不同的是, 得到的是 **所有** 符合条件的元素.
    #. :func:`DOM.attr(elem, name, val) <DOM.attr>`, 获取/设置元素某个属性, 这里, 在动画开始前给按钮设置不可用状态.
    #. :mod:`Anim`, 提供动画效果, 通过给元素设定参数, 就可以让这个元素动态地从当前参数变化到设定的目标参数.
    #. :func:`DOM.get`/:func:`DOM.query` 也可以直接用 ``S.get/S.query`` 来调用, 是一样的.


``DOM/Event`` 是最基本的功能, 掌握了这两个, 就能基本使用 KISSY 了.
接下来将介绍 :ref:`Node <quickstart-usenode>` 对象的使用.



.. rubric:: 参考链接

.. [1] `DOM API 文档 <dom>`_
.. [2] `Event API 文档 <event>`_

