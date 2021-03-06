.. currentmodule:: Editor

FAQ
===========

数据同步
-----------------

form 同步
~~~~~~~~~~~~~~~~~~~~~~~

	如果后端通过 form 提交(submit)来获得用户输入数据, 则只需配置参数 :class:`attachForm <Editor.KISSY.Editor>`  .
	
	.. code-block:: javascript

  		//是否监控编辑器所属的表单提交
  		"attachForm":true,

	编辑器自动会监控 form 的 sbumit 事件进行同步


手动同步
~~~~~~~~~~~~~~~~~~~~~~~

	涉及三个 api
	
	editor 为调用 KISSY.Editor 返回的编辑器实例

	``editor.sync()`` : 手动同步编辑器内容到对应 textarea

	``editor.getData()`` : 获得当前编辑器的内容

	``editor.setData(html:string)`` :设置当前编辑器的内容, 参数为html, 类型为 string 字符串

自动保存
-----------------
	
	自动保存为 localStorage/flash 机制, 保存在本地, 可 :attr:`配置参数 <pluginConfig.draft>` .

字数统计
-------------------

    可参考以下 demo  :

    http://docs.kissyui.com/kissy-editor/demo/cdn/1.1.7/wordCount.html

    其中 `wordcount 代码 <http://docs.kissyui.com/kissy-editor/demo/word-count.js>`_ 自行下载, 随意修改.
	
绑定 ctrol-enter
----------------------------------

不少的应用场景要求在编辑器编辑区域内按下 ctrol+enter 按键时, 编辑器所在表单会自动提交, 解决方案是监控编辑器的文档按键事件：
    
    
.. code-block:: javascript
    
    editor.ready(function () {
        KISSY.Event.on(editor.document, "keydown", function (ev) {
            if (ev.keyCode == 13 && ev.ctrlKey) {
                editor.sync();
                editor.textarea[0].form.submit();
    
            }
        })
    });	
    
其中 editor 为编辑器实例的对象, 通过 ``var editor=KISSY.Editor("#id",cfg)`` 获取而来.


placeholder(tip) 功能
-------------------------------

    可参考以下 demo  :

    http://docs.kissyui.com/kissy-editor/demo/cdn/1.1.7/tip.html

    其中 `tip 代码 <http://docs.kissyui.com/kissy-editor/demo/tip.js>`_ 自行下载，随意修改。
    
    
截获 paste 事件
---------------------------------------

可以通过监听编辑器实例对象的 "paste" 事件来截获用户粘贴的内容

.. code-block:: javascript

    var editor=KISSY.Editor(..);
    editor.on("paste",function(ev){
        var html=ev.html;// 用户的原始粘贴内容
        // do sth to html
        html="changed";
        return html;  // 返回修改后的粘贴内容        
    });     
