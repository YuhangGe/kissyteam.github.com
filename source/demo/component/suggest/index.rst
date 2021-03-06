﻿.. py:currentmodule:: Suggest

Suggest Demos
======================================

|  作者: `玉伯 <lifesinger@gmail.com>`_
|  `源码 <https://github.com/kissyteam/kissy/tree/master/src/suggest/>`_

Class
-----------------------------------------------

  * :class:`Suggest`

.. _Component-suggest-demo0:

Demo - 基本使用示例
--------------------------------------------------

待补充

.. _Component-suggest-demo1:

Demo - 淘宝首页的搜索提示
--------------------------------------------------

    .. raw:: html

        <style>
            .section {
                margin: 20px;
            }

            .search-input {
                height: 20px;
                padding: 3px 2px 2px 4px;
                width: 300px;
                border: 1px solid #999;
            }
            .tb-srch-may .rc-lt,
            .tb-srch-may .rc-lb,
            .tb-srch-may .rc-rb,
            .tb-srch-may .rc-rt {
                font-size: 0;
                font-family: serif;
                width: 1px;
                height: 1px;
                position: absolute;
                background-color: #fff;
            }
            .tb-srch-may .rc-lt {
                left: 0;
                top: 0;
            }

            .tb-srch-may .rc-lb {
                left: 0;
                bottom: 0;
            }

            .tb-srch-may .rc-rb {
                right: 0;
                bottom: 0;
            }

            .tb-srch-may .rc-rt {
                right: 0;
                top: 0;
            }
            .tb-srch-may .tb-srch-may-tab {
                float:left;
                height: 23px;
            }

            .tb-srch-may .tb-srch-may-tab li {
                float: left;
                position: relative;
            }
            .tb-srch-may .tb-srch-may-tab li .rc-lt,
            .tb-srch-may .tb-srch-may-tab li .rc-rt {
                display: none;
            }

            .tb-srch-may .tb-srch-may-tab .current .rc-lt,
            .tb-srch-may .tb-srch-may-tab .current .rc-rt {
                display: block;
                background-color: #ffdebb;
            }

            .tb-srch-may .tb-srch-may-tab li a {
                display: block;
                float: left;
                height: 23px;
                line-height: 23px;
                padding: 0 15px;
            }

            .tb-srch-may .tb-srch-may-tab li.current a {
                font-weight: bold;
                color: #fff;
                background-color: #f27b04;
            }
            .tb-srch-may .tb-srch-may-panel {
                clear: left;
            }
        </style>
        <div class="section">
                <div class="tb-srch-may" id="J_TBSearch">
                    <ul class="tb-srch-may-tab ks-clear">
                        <li class="current"><a href="http://list.taobao.com/browse/cat-0.htm">宝贝</a><b class="rc-lt"></b><b class="rc-rt"></b></li>
                        <li><a href="http://shopsearch.taobao.com/browse/shop_search.htm">商城</a><b class="rc-lt"></b><b class="rc-rt"></b></li>
                    </ul>
                    <div class="tb-srch-may-panel ks-clear">
                        <form name="search" method="get" action="http://search1.taobao.com/browse/search_auction.htm">
                            <input type="hidden" value="" name="sort"/>
                            <input type="hidden" value="D9_5_1" name="f"/>
                            <input type="hidden" value="" name="promote"/>
                            <input type="hidden" value="2" name="isnew"/>
                            <input type="hidden" value="b" name="atype"/>
                            <input type="hidden" value="all" name="commend"/>
                            <input type="hidden" value="auction" name="search_type"/>
                            <input type="hidden" value="initiative" name="user_action"/>
                            <input type="hidden" value="s1-e" name="ssid"/>

                            <input name="q" id="qstab" class="search-input"/>

                            <button type="submit" class="search-submit">淘我喜欢</button>
                        </form>
                    </div>
                </div>
                <script>
                    KISSY.use("node,suggest", function(S, Node, Suggest) {
                        // 1.1.6
                        Node = S.Node;
                        Suggest = S.Suggest;

                        var _suggest = new Suggest('#qstab', 'http://suggest.taobao.com/sug?code=utf-8&extras=1', {
                                    resultFormat: '约%result%个宝贝',
                                    dataType: 1
                                }),
                                tab = S.one('.tb-srch-may-tab'),
                                tabList = tab.all('li'),
                                switchToTab = function(n) {
                                    _suggest.config.resultFormat = '约%result%个宝贝';
                                    if (n == 1) {
                                        _suggest.dataSource = 'http://suggest.taobao.com/sug?area=b2c&code=utf-8&extras=1&callback=KISSY.Suggest.callback';
                                        _suggest.config.resultFormat = '约%result%个商品';
                                    } else {
                                        _suggest.dataSource = 'http://suggest.taobao.com/sug?code=utf-8&extras=1&callback=KISSY.Suggest.callback';
                                    }
                                    S.each(tabList, function(tab, i) {
                                        tab = new Node(tab);

                                        tab[(i == n) ? "addClass" : "removeClass"]('current');
                                    });
                                };

                        // on tabs switch
                        S.each(tabList, function(tab, i) {
                            tab = new Node(tab);
                            tab.on("click", function(ev) {
                                ev.halt();
                                switchToTab(i);
                            });
                        });
                    });
                </script>
            </div>


    .. code-block:: javascript

        KISSY.use("node,suggest", function(S, Node, Suggest) {
            // 如果是 1.1.6, Node 和Suggest 都是直接在 KISSY 上的
            Node = S.Node;
            Suggest = S.Suggest;

            var _suggest = new Suggest('#qstab', 'http://suggest.taobao.com/sug?code=utf-8&extras=1', {
                        resultFormat: '约%result%个宝贝',
                        dataType: 1
                    }),
                tab = S.one('.tb-srch-may-tab'),
                tabList = tab.all('li'),
                switchToTab = function(n) {
                    // 动态设置数据源和结果格式
                    _suggest.config.resultFormat = '约%result%个宝贝';
                    if (n == 1) {
                        _suggest.dataSource = 'http://suggest.taobao.com/sug?area=b2c&code=utf-8&extras=1&callback=KISSY.Suggest.callback';
                        _suggest.config.resultFormat = '约%result%个商品';
                    } else {
                        _suggest.dataSource = 'http://suggest.taobao.com/sug?code=utf-8&extras=1&callback=KISSY.Suggest.callback';
                    }
                    S.each(tabList, function(tab, i) {
                        tab = new Node(tab);

                        tab[(i == n) ? "addClass" : "removeClass"]('current');
                    });
                };

            // tab切换
            S.each(tabList, function(tab, i) {
                tab = new Node(tab);
                tab.on("click", function(ev) {
                    ev.halt();
                    switchToTab(i);
                });
            });
        });

.. _Component-suggest-demo2:

Demo - 有啊首页的搜索提示
--------------------------------------------------

    .. raw:: html

        <div class="section">
            <form name="search2" method="get" action="http://youa.baidu.com/search/s" target="_blank">
                <input class="search-input" name="keyword" id="q2"/>
                <button type="submit" class="search-submit">百度一下</button>
            </form>
            <style>
                .youa-suggest-container {
                    border-color: #5BA515
                }

                .youa-suggest-container li {
                    padding: 2px 0 3px;
                    font-size: 14px;
                    line-height: 20px
                }

                .youa-suggest-container .ks-selected {
                    background-color: #DEEFC5
                }

                .youa-suggest-container .ks-suggest-result {
                    font-size: 12px;
                    color: #999
                }

                .youa-suggest-container .ks-selected span {
                    color: #240055
                }

                .youa-suggest-container .ks-selected .ks-suggest-result {
                    color: #999
                }
            </style>
            <script>
                KISSY.use("suggest", function(S, Suggest) {
                        // 1.1.6
                        Suggest = S.Suggest;

                        // 有啊
                        // http://youa.baidu.com/suggest/se/s?cmd=suggest&type=kwd&max_count=10&callback=suggestCallback&keyword=n
                        var dataUrl = 'http://youa.baidu.com/suggest/se/s?cmd=suggest&type=kwd&max_count=10';
                        var sug = new Suggest('#q2', dataUrl, {
                            containerCls: 'youa-suggest-container',
                            charset: 'gbk',
                            callbackFn: 'suggestCallback',
                            queryName: 'keyword'
                        });

                        // youa: suggestCallback({"err":"ok", "r":[{"key":"nike", "val":140000}, {"key":"nike鞋", "val":119000}, {"key":"nike板鞋", "val":44300}, {"key":"nike运动鞋", "val":115000}, {"key":"nike正品", "val":47400}, {"key":"nike包", "val":8300}, {"key":"nike篮球鞋", "val":18400}, {"key":"nike新款", "val":27600}, {"key":"nike 耐克", "val":140000}, {"key":"nike女鞋", "val":7850}], "num":10})
                        // taobao: g_ks_suggest_callback({"result": [["nike 正品", "2170000"], ["nike 专柜 正品", "834000"], ["nike 短袖", "242000"], ["nike 板 鞋", "989000"], ["nike 女鞋", "253000"], ["nike 运动鞋", "550000"], ["nike 包", "295000"], ["nike 鞋", "3160000"], ["nike 单肩包", "38500"], ["nike 09", "786000"]]})
                        sug.on('dataReturn', function() {
                            var data = this.returnedData['r'] || [], result = [];

                            for (var i = 0, len = data.length; i < len; ++i) {
                                result.push([data[i]['key'], data[i]['val']]);
                            }
                            this.returnedData = result;
                        });
                });
            </script>
        </div>

    .. code-block:: javascript

        KISSY.use("suggest", function(S, Suggest) {
            // 1.1.6
            Suggest = S.Suggest;

            // 有啊
            // http://youa.baidu.com/suggest/se/s?cmd=suggest&type=kwd&max_count=10&callback=suggestCallback&keyword=n
            var dataUrl = 'http://youa.baidu.com/suggest/se/s?cmd=suggest&type=kwd&max_count=10';
            var sug = new Suggest('#q2', dataUrl, {
                containerCls: 'youa-suggest-container',
                charset: 'gbk',
                callbackFn: 'suggestCallback',
                queryName: 'keyword'
            });

            // youa: suggestCallback({"err":"ok", "r":[{"key":"nike", "val":140000}, {"key":"nike鞋", "val":119000}, {"key":"nike板鞋", "val":44300}, {"key":"nike运动鞋", "val":115000}, {"key":"nike正品", "val":47400}, {"key":"nike包", "val":8300}, {"key":"nike篮球鞋", "val":18400}, {"key":"nike新款", "val":27600}, {"key":"nike 耐克", "val":140000}, {"key":"nike女鞋", "val":7850}], "num":10})
            // taobao: g_ks_suggest_callback({"result": [["nike 正品", "2170000"], ["nike 专柜 正品", "834000"], ["nike 短袖", "242000"], ["nike 板 鞋", "989000"], ["nike 女鞋", "253000"], ["nike 运动鞋", "550000"], ["nike 包", "295000"], ["nike 鞋", "3160000"], ["nike 单肩包", "38500"], ["nike 09", "786000"]]})
            sug.on('dataReturn', function() {
                var data = this.returnedData['r'] || [], result = [];

                for (var i = 0, len = data.length; i < len; ++i) {
                    result.push([data[i]['key'], data[i]['val']]);
                }
                this.returnedData = result;
            });
        });

.. _Component-suggest-demo3:

Demo - 百度的搜索提示
--------------------------------------------------

    .. raw:: html

        <div class="section">
            <style>

            .bd-sug {
                border-color: #666
            }

            .bd-sug li {
                padding: 2px 0 3px
            }

            .bd-sug .ks-selected {
                background-color: #D5E2FF
            }

            .bd-sug .ks-selected span {
                color: #240055
            }
        </style>
            <div id="bds">
                <form action="s" name="f">
                    <input class="search-input" type="text" maxlength="100" id="kw" name="wd" autocomplete="off">
                    <input type="submit" id="su" value="百度一下">
                </form>
            </div>

            <script>
                KISSY.use("suggest", function(S,Suggest) {
                    // 1.1.6
                    Suggest = S.Suggest;

                    // Baidu
                    var dataUrl = 'http://suggestion.baidu.com/su?p=3&cb=window.bdsug.sug';
                    var sug = new Suggest('#kw', dataUrl, {
                        resultFormat: '',
                        containerCls: 'bd-sug',
                        charset: 'gb2312',
                        queryName: 'wd',
                        callbackFn: 'bdsug.sug'
                    });

                    // baidu: window.bdsug.sug({q:"nike",p:true,s:["nike官网","妮可基德曼","妮可","妮可罗宾","妮可里奇","nike鞋","nike 官网","尼可","nike女","nike360"]});
                    // taobao: g_ks_suggest_callback({"result": [["nike 正品", "2170000"], ["nike 专柜 正品", "834000"], ["nike 短袖", "242000"], ["nike 板 鞋", "989000"], ["nike 女鞋", "253000"], ["nike 运动鞋", "550000"], ["nike 包", "295000"], ["nike 鞋", "3160000"], ["nike 单肩包", "38500"], ["nike 09", "786000"]]})
                    sug.on('dataReturn', function() {
                        this.returnedData = this.returnedData.s || [];
                    });
                });
            </script>
        </div>


    .. code-block:: javascript

        KISSY.use("suggest", function(S,Suggest) {
            // 1.1.6
            Suggest = S.Suggest;

            // Baidu
            var dataUrl = 'http://suggestion.baidu.com/su?p=3&cb=window.bdsug.sug';
            var sug = new Suggest('#kw', dataUrl, {
                resultFormat: '',
                containerCls: 'bd-sug',
                charset: 'gb2312',
                queryName: 'wd',
                callbackFn: 'bdsug.sug'
            });

            // baidu: window.bdsug.sug({q:"nike",p:true,s:["nike官网","妮可基德曼","妮可","妮可罗宾","妮可里奇","nike鞋","nike 官网","尼可","nike女","nike360"]});
            // taobao: g_ks_suggest_callback({"result": [["nike 正品", "2170000"], ["nike 专柜 正品", "834000"], ["nike 短袖", "242000"], ["nike 板 鞋", "989000"], ["nike 女鞋", "253000"], ["nike 运动鞋", "550000"], ["nike 包", "295000"], ["nike 鞋", "3160000"], ["nike 单肩包", "38500"], ["nike 09", "786000"]]})
            sug.on('dataReturn', function() {
                this.returnedData = this.returnedData.s || [];
            });
        });

.. _Component-suggest-demo4:

Demo - Google 的搜索提示
--------------------------------------------------

    .. raw:: html

            <div class="section" style="width: 380px">
                <form name="f" action="http://www.google.com/search">
                    <table cellspacing="0" cellpadding="0">
                        <tbody>
                        <tr valign="top">
                            <td width="25%"></td>
                            <td nowrap="" align="center">
                                <input type="hidden" value="en" name="hl"/>
                                <input class="search-input" value="" title="Google Search" size="55" id="gq" name="q" maxlength="2048" autocomplete="off"/>
                                <br/>
                                <input type="submit" class="g-submit" onclick="this.checked=1" value="Google Search" name="btnG"/>
                                <input type="submit" class="g-submit" onclick="this.checked=1" value="I'm Feeling Lucky" name="btnI"/>
                            </td>
                        </tr>
                        </tbody>
                    </table>
                    <input type="hidden" name="aq" value="f"/><input type="hidden" name="oq" value="n"/><input type="hidden" name="aqi" value="g10"/>
                </form>
                <style>
                    .g-sug {
                        border-color: #666
                    }

                    .g-sug li {
                        padding: 2px 0 3px
                    }

                    .g-sug .ks-selected {
                        background-color: #D5E2FF
                    }

                    .g-sug .ks-selected span {
                        color: #240055
                    }
                </style>
                <script>
                    KISSY.use("suggest", function(S, Suggest) {
                        // 1.1.6
                        Suggest = S.Suggest;
                        // Google
                        var dataUrl = 'http://clients1.google.com/complete/search?hl=en';
                        var sug = new Suggest('#gq', dataUrl, {
                            resultFormat: '',
                            containerCls: 'g-sug',
                            callbackFn: 'google.ac.h'
                        });

                        // google: window.google.ac.h(["ni",[["牛博网","73,248 结果","0z"],["牛博网首页","12,200,617 结果","1z"],["你是准备替党说话 还是准备替老百姓说话","136,545 结果","2z"],["nike","117,000,000 结果","3"],["nikon","127,000,000 结果","4"],["nissan","135,000,000 结果","5"],["nine west","40,000,000 结果","6"],["nike鞋","3,380,000 结果","7"],["倪萍 再婚","36,400 结果","8"],["牛年祝福语","582,000 结果","9"]]])
                        // taobao: g_ks_suggest_callback({"result": [["nike 正品", "2170000"], ["nike 专柜 正品", "834000"], ["nike 短袖", "242000"], ["nike 板 鞋", "989000"], ["nike 女鞋", "253000"], ["nike 运动鞋", "550000"], ["nike 包", "295000"], ["nike 鞋", "3160000"], ["nike 单肩包", "38500"], ["nike 09", "786000"]]})
                        sug.on('dataReturn', function() {
                            this.returnedData = this.returnedData[1] || [];
                        });

                    });
                </script>
            </div>

    .. code-block:: javascript

        KISSY.use("suggest", function(S, Suggest) {
            // 1.1.6
            Suggest = S.Suggest;
            // Google
            var dataUrl = 'http://clients1.google.com/complete/search?hl=en';
            var sug = new Suggest('#gq', dataUrl, {
                resultFormat: '',
                containerCls: 'g-sug',
                callbackFn: 'google.ac.h'
            });

            // google: window.google.ac.h(["ni",[["牛博网","73,248 结果","0z"],["牛博网首页","12,200,617 结果","1z"],["你是准备替党说话 还是准备替老百姓说话","136,545 结果","2z"],["nike","117,000,000 结果","3"],["nikon","127,000,000 结果","4"],["nissan","135,000,000 结果","5"],["nine west","40,000,000 结果","6"],["nike鞋","3,380,000 结果","7"],["倪萍 再婚","36,400 结果","8"],["牛年祝福语","582,000 结果","9"]]])
            // taobao: g_ks_suggest_callback({"result": [["nike 正品", "2170000"], ["nike 专柜 正品", "834000"], ["nike 短袖", "242000"], ["nike 板 鞋", "989000"], ["nike 女鞋", "253000"], ["nike 运动鞋", "550000"], ["nike 包", "295000"], ["nike 鞋", "3160000"], ["nike 单肩包", "38500"], ["nike 09", "786000"]]})
            sug.on('dataReturn', function() {
                this.returnedData = this.returnedData[1] || [];
            });

        });