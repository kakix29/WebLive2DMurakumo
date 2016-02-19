# WebLive2DMurakumo
<meta charset="utf-8" />
<p>demo预览：http://www.kakinuma.date/l2d.html</p>
<p>官方：http://www.live2d.com/en/</p>
<p>sdk下载：https://link.zhihu.com/?target=http%3A//app2.live2d.com/cubism/sdk/bowiuex/webgl/Live2D_SDK_WebGL_2.0.05_1_en.zip</p>
<p>sdk目录：</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160219010434441-1359811605.png" alt="" width="488" height="577" /></p>
<p>framework框架有一个js，lib库有1个，这是最基本的构成</p>
<p>下面有SampleApp1，Simple两个例子，simple是前者的精简版，只有显示没有功能，就不看它了</p>
<p>SampleApp1中</p>
<p>assets包括了背景和模型等资源</p>
<p>src则是模型的初始化，显示，事件绑定等等的功能实现代码</p>
<p>&nbsp;</p>
<p>首先为了测试，先导进了所有的.js，然后添加个标签</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE HTML</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">='lib/live2d.min.js'</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">='framework/Live2DFramework.js'</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/utils/MatrixStack.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/utils/ModelSettingJson.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/PlatformManager.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/LAppDefine.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/LAppModel.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/LAppLive2DManager.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/SampleApp1.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>


<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">canvas </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="test"</span><span style="color: #ff0000;"> width</span><span style="color: #0000ff;">="450px"</span><span style="color: #ff0000;"> height</span><span style="color: #0000ff;">="500px"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="position:fixed;right:0px;bottom:-10px;"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">canvas</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">
      sampleApp1();
    </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>.js 文件都按路径放好就好了</p>
<p>然后试着打开页面，看看报错（压根就没觉得可以直接用,因为我压根就没有添加模型文件</p>
<p><img src="http://img.blog.csdn.net/20160218230415859?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt="" width="1709" height="119" /></p>
<p>init&hellip;&hellip;应该是初始化有错，具体看看</p>
<p><img src="http://img.blog.csdn.net/20160218230509542?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt="" width="1434" height="128" /></p>
<p><br />说是null了应该是没传到参数，所以参数canvasId应该是有问题（顺便Canvas在这应该是画布的意思）</p>
<p>&nbsp;</p>
<p>顶上面一行，getId出错，那就应该是html里id没写对&hellip;&hellip;随手写了个test确实太随意了&hellip;&hellip;</p>
<p>这个canvasId的来源就在这函数头顶上，就是初始化的Sample1()</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160218231712269-1745399368.png" alt="" width="572" height="578" /></p>
<p>改一下，改成glcanvas，改掉以后出现了新的错误，是同样类别的错误，因为官方Sample里有换模型的按钮，所以我没写，Id一样没get到，但是我不想使用换模型的功能，所以我尝试不使用者这功能</p>
<p>所以在初始化函数SampleApp1()中调用的init中，选择不要那个Button</p>
<p>然后所有的change的地方都暂时选择注释掉，地方不少&hellip;&hellip;change的定义，和一些调用，因为Sample中右键模型也是可以change的</p>
<p>然后问题没了，但是理所当然是空白，因为我没加模型</p>
<p>不过审查元素的话，元素是在的（当然在了</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160218232737222-228268187.png" alt="" width="907" height="423" /></p>
<p>现在的SampleApp1.js被修改为</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> thisRef = <span style="color: #0000ff;">this</span><span style="color: #000000;">;


window.onerror </span>= <span style="color: #0000ff;">function</span><span style="color: #000000;">(msg, url, line, col, error) {
    </span><span style="color: #0000ff;">var</span> errmsg = "file:" + url + "&lt;br&gt;line:" + line + " " +<span style="color: #000000;"> msg;
    l2dError(errmsg);
}

</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> SampleApp1()
{
    </span><span style="color: #0000ff;">this</span>.platform =<span style="color: #000000;"> window.navigator.platform.toLowerCase();
    
    </span><span style="color: #0000ff;">this</span>.live2DMgr = <span style="color: #0000ff;">new</span><span style="color: #000000;"> LAppLive2DManager();

    </span><span style="color: #0000ff;">this</span>.isDrawStart = <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    
    </span><span style="color: #0000ff;">this</span>.gl = <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.canvas = <span style="color: #0000ff;">null</span><span style="color: #000000;">;
    
    </span><span style="color: #0000ff;">this</span>.dragMgr = <span style="color: #0000ff;">null</span>; <span style="color: #008000;">/*</span><span style="color: #008000;">new L2DTargetPoint();</span><span style="color: #008000;">*/</span> 
    <span style="color: #0000ff;">this</span>.viewMatrix = <span style="color: #0000ff;">null</span>; <span style="color: #008000;">/*</span><span style="color: #008000;">new L2DViewMatrix();</span><span style="color: #008000;">*/</span>
    <span style="color: #0000ff;">this</span>.projMatrix = <span style="color: #0000ff;">null</span>; <span style="color: #008000;">/*</span><span style="color: #008000;">new L2DMatrix44()</span><span style="color: #008000;">*/</span>
    <span style="color: #0000ff;">this</span>.deviceToScreen = <span style="color: #0000ff;">null</span>; <span style="color: #008000;">/*</span><span style="color: #008000;">new L2DMatrix44();</span><span style="color: #008000;">*/</span>
    
    <span style="color: #0000ff;">this</span>.drag = <span style="color: #0000ff;">false</span><span style="color: #000000;">; 
    </span><span style="color: #0000ff;">this</span>.oldLen = 0<span style="color: #000000;">;    
    
    </span><span style="color: #0000ff;">this</span>.lastMouseX = 0<span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.lastMouseY = 0<span style="color: #000000;">;
    
    </span><span style="color: #0000ff;">this</span>.isModelShown = <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    
    
    initL2dCanvas(</span>"glCanvas"<span style="color: #000000;">);
    
    
    init();
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> initL2dCanvas(canvasId)
{
    
    </span><span style="color: #0000ff;">this</span>.canvas =<span style="color: #000000;"> document.getElementById(canvasId);
    
    
    </span><span style="color: #0000ff;">if</span>(<span style="color: #0000ff;">this</span><span style="color: #000000;">.canvas.addEventListener) {
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("mousewheel", mouseEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("click", mouseEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("mousedown", mouseEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("mousemove", mouseEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("mouseup", mouseEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("mouseout", mouseEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("contextmenu", mouseEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        
        
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("touchstart", touchEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("touchend", touchEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        </span><span style="color: #0000ff;">this</span>.canvas.addEventListener("touchmove", touchEvent, <span style="color: #0000ff;">false</span><span style="color: #000000;">);
        
    }
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> init()
{    
    
    </span><span style="color: #0000ff;">var</span> width = <span style="color: #0000ff;">this</span><span style="color: #000000;">.canvas.width;
    </span><span style="color: #0000ff;">var</span> height = <span style="color: #0000ff;">this</span><span style="color: #000000;">.canvas.height;
    
    </span><span style="color: #0000ff;">this</span>.dragMgr = <span style="color: #0000ff;">new</span><span style="color: #000000;"> L2DTargetPoint();

    
    </span><span style="color: #0000ff;">var</span> ratio = height /<span style="color: #000000;"> width;
    </span><span style="color: #0000ff;">var</span> left =<span style="color: #000000;"> LAppDefine.VIEW_LOGICAL_LEFT;
    </span><span style="color: #0000ff;">var</span> right =<span style="color: #000000;"> LAppDefine.VIEW_LOGICAL_RIGHT;
    </span><span style="color: #0000ff;">var</span> bottom = -<span style="color: #000000;">ratio;
    </span><span style="color: #0000ff;">var</span> top =<span style="color: #000000;"> ratio;

    </span><span style="color: #0000ff;">this</span>.viewMatrix = <span style="color: #0000ff;">new</span><span style="color: #000000;"> L2DViewMatrix();

    
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.viewMatrix.setScreenRect(left, right, bottom, top);
    
    
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.viewMatrix.setMaxScreenRect(LAppDefine.VIEW_LOGICAL_MAX_LEFT,
                                     LAppDefine.VIEW_LOGICAL_MAX_RIGHT,
                                     LAppDefine.VIEW_LOGICAL_MAX_BOTTOM,
                                     LAppDefine.VIEW_LOGICAL_MAX_TOP); 

    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.viewMatrix.setMaxScale(LAppDefine.VIEW_MAX_SCALE);
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.viewMatrix.setMinScale(LAppDefine.VIEW_MIN_SCALE);

    </span><span style="color: #0000ff;">this</span>.projMatrix = <span style="color: #0000ff;">new</span><span style="color: #000000;"> L2DMatrix44();
    </span><span style="color: #0000ff;">this</span>.projMatrix.multScale(1, (width /<span style="color: #000000;"> height));

    
    </span><span style="color: #0000ff;">this</span>.deviceToScreen = <span style="color: #0000ff;">new</span><span style="color: #000000;"> L2DMatrix44();
    </span><span style="color: #0000ff;">this</span>.deviceToScreen.multTranslate(-width / 2.0, -height / 2.0<span style="color: #000000;">);
    </span><span style="color: #0000ff;">this</span>.deviceToScreen.multScale(2 / width, -2 /<span style="color: #000000;"> width);
    
    
    
    </span><span style="color: #0000ff;">this</span>.gl =<span style="color: #000000;"> getWebGLContext();
    </span><span style="color: #0000ff;">if</span> (!<span style="color: #0000ff;">this</span><span style="color: #000000;">.gl) {
        l2dError(</span>"Failed to create WebGL context."<span style="color: #000000;">);
        </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
    }

    
    </span><span style="color: #0000ff;">this</span>.gl.clearColor(0.0, 0.0, 0.0, 0.0<span style="color: #000000;">);

    changeModel();
    
    startDraw();
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> startDraw() {
    </span><span style="color: #0000ff;">if</span>(!<span style="color: #0000ff;">this</span><span style="color: #000000;">.isDrawStart) {
        </span><span style="color: #0000ff;">this</span>.isDrawStart = <span style="color: #0000ff;">true</span><span style="color: #000000;">;
        (</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> tick() {
                draw(); 

                </span><span style="color: #0000ff;">var</span> requestAnimationFrame =<span style="color: #000000;"> 
                    window.requestAnimationFrame </span>||<span style="color: #000000;"> 
                    window.mozRequestAnimationFrame </span>||<span style="color: #000000;">
                    window.webkitRequestAnimationFrame </span>||<span style="color: #000000;"> 
                    window.msRequestAnimationFrame;

                
                requestAnimationFrame(tick ,</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.canvas);   
        })();
    }
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> draw()
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> l2dLog("--&gt; draw()");</span>
<span style="color: #000000;">
    MatrixStack.reset();
    MatrixStack.loadIdentity();
    
    </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.dragMgr.update(); 
    </span><span style="color: #0000ff;">this</span>.live2DMgr.setDrag(<span style="color: #0000ff;">this</span>.dragMgr.getX(), <span style="color: #0000ff;">this</span><span style="color: #000000;">.dragMgr.getY());
    
    
    </span><span style="color: #0000ff;">this</span>.gl.clear(<span style="color: #0000ff;">this</span><span style="color: #000000;">.gl.COLOR_BUFFER_BIT);
    
    MatrixStack.multMatrix(projMatrix.getArray());
    MatrixStack.multMatrix(viewMatrix.getArray());
    MatrixStack.push();
    
    </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">var</span> i = 0; i &lt; <span style="color: #0000ff;">this</span>.live2DMgr.numModels(); i++<span style="color: #000000;">)
    {
        </span><span style="color: #0000ff;">var</span> model = <span style="color: #0000ff;">this</span><span style="color: #000000;">.live2DMgr.getModel(i);

        </span><span style="color: #0000ff;">if</span>(model == <span style="color: #0000ff;">null</span>) <span style="color: #0000ff;">return</span><span style="color: #000000;">;
        
        </span><span style="color: #0000ff;">if</span> (model.initialized &amp;&amp; !<span style="color: #000000;">model.updating)
        {
            model.update();
            model.draw(</span><span style="color: #0000ff;">this</span><span style="color: #000000;">.gl);
            
            </span><span style="color: #0000ff;">if</span> (!<span style="color: #0000ff;">this</span>.isModelShown &amp;&amp; i == <span style="color: #0000ff;">this</span>.live2DMgr.numModels()-1<span style="color: #000000;">) {
                </span><span style="color: #0000ff;">this</span>.isModelShown = !<span style="color: #0000ff;">this</span><span style="color: #000000;">.isModelShown;
            }
        }
    }
    
    MatrixStack.pop();
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> changeModel()
{
    </span><span style="color: #0000ff;">this</span>.isModelShown = <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    
    </span><span style="color: #0000ff;">this</span>.live2DMgr.reloadFlg = <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    </span><span style="color: #0000ff;">this</span>.live2DMgr.count++<span style="color: #000000;">;

    </span><span style="color: #0000ff;">this</span>.live2DMgr.changeModel(<span style="color: #0000ff;">this</span><span style="color: #000000;">.gl);
}




</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> modelScaling(scale)
{   
    </span><span style="color: #0000ff;">var</span> isMaxScale =<span style="color: #000000;"> thisRef.viewMatrix.isMaxScale();
    </span><span style="color: #0000ff;">var</span> isMinScale =<span style="color: #000000;"> thisRef.viewMatrix.isMinScale();
    
    thisRef.viewMatrix.adjustScale(</span>0, 0<span style="color: #000000;">, scale);

    
    </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">isMaxScale)
    {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (thisRef.viewMatrix.isMaxScale())
        {
            thisRef.live2DMgr.maxScaleEvent();
        }
    }
    
    </span><span style="color: #0000ff;">if</span> (!<span style="color: #000000;">isMinScale)
    {
        </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (thisRef.viewMatrix.isMinScale())
        {
            thisRef.live2DMgr.minScaleEvent();
        }
    }
}



</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> modelTurnHead(event)
{
    thisRef.drag </span>= <span style="color: #0000ff;">true</span><span style="color: #000000;">;
    
    </span><span style="color: #0000ff;">var</span> rect =<span style="color: #000000;"> event.target.getBoundingClientRect();
    
    </span><span style="color: #0000ff;">var</span> sx = transformScreenX(event.clientX -<span style="color: #000000;"> rect.left);
    </span><span style="color: #0000ff;">var</span> sy = transformScreenY(event.clientY -<span style="color: #000000;"> rect.top);
    </span><span style="color: #0000ff;">var</span> vx = transformViewX(event.clientX -<span style="color: #000000;"> rect.left);
    </span><span style="color: #0000ff;">var</span> vy = transformViewY(event.clientY -<span style="color: #000000;"> rect.top);
    
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_MOUSE_LOG)
        l2dLog(</span>"onMouseDown device( x:" + event.clientX + " y:" + event.clientY + " ) view( x:" + vx + " y:" + vy + ")"<span style="color: #000000;">);

    thisRef.lastMouseX </span>=<span style="color: #000000;"> sx;
    thisRef.lastMouseY </span>=<span style="color: #000000;"> sy;

    thisRef.dragMgr.setPoint(vx, vy); 
    
    
    thisRef.live2DMgr.tapEvent(vx, vy);
}



</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> followPointer(event)
{    
    </span><span style="color: #0000ff;">var</span> rect =<span style="color: #000000;"> event.target.getBoundingClientRect();
    
    </span><span style="color: #0000ff;">var</span> sx = transformScreenX(event.clientX -<span style="color: #000000;"> rect.left);
    </span><span style="color: #0000ff;">var</span> sy = transformScreenY(event.clientY -<span style="color: #000000;"> rect.top);
    </span><span style="color: #0000ff;">var</span> vx = transformViewX(event.clientX -<span style="color: #000000;"> rect.left);
    </span><span style="color: #0000ff;">var</span> vy = transformViewY(event.clientY -<span style="color: #000000;"> rect.top);
    
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_MOUSE_LOG)
        l2dLog(</span>"onMouseMove device( x:" + event.clientX + " y:" + event.clientY + " ) view( x:" + vx + " y:" + vy + ")"<span style="color: #000000;">);

    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (thisRef.drag)
    {
        thisRef.lastMouseX </span>=<span style="color: #000000;"> sx;
        thisRef.lastMouseY </span>=<span style="color: #000000;"> sy;

        thisRef.dragMgr.setPoint(vx, vy); 
    }
}

        

</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> lookFront()
{   
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (thisRef.drag)
    {
        thisRef.drag </span>= <span style="color: #0000ff;">false</span><span style="color: #000000;">;
    }

    thisRef.dragMgr.setPoint(</span>0, 0<span style="color: #000000;">);
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> mouseEvent(e)
{
    e.preventDefault();
    
    </span><span style="color: #0000ff;">if</span> (e.type == "mousewheel"<span style="color: #000000;">) {

        </span><span style="color: #0000ff;">if</span> (e.clientX &lt; 0 || thisRef.canvas.clientWidth &lt; e.clientX ||<span style="color: #000000;"> 
        e.clientY </span>&lt; 0 || thisRef.canvas.clientHeight &lt;<span style="color: #000000;"> e.clientY)
        {
            </span><span style="color: #0000ff;">return</span><span style="color: #000000;">;
        }
        
        </span><span style="color: #0000ff;">if</span> (e.wheelDelta &gt; 0) modelScaling(1.1<span style="color: #000000;">); 
        </span><span style="color: #0000ff;">else</span> modelScaling(0.9<span style="color: #000000;">); 

        
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (e.type == "mousedown"<span style="color: #000000;">) {

        
        </span><span style="color: #0000ff;">if</span>("button" <span style="color: #0000ff;">in</span> e &amp;&amp; e.button != 0) <span style="color: #0000ff;">return</span><span style="color: #000000;">;
        
        modelTurnHead(e);
        
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (e.type == "mousemove"<span style="color: #000000;">) {
        
        followPointer(e);
        
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (e.type == "mouseup"<span style="color: #000000;">) {
        
        
        </span><span style="color: #0000ff;">if</span>("button" <span style="color: #0000ff;">in</span> e &amp;&amp; e.button != 0) <span style="color: #0000ff;">return</span><span style="color: #000000;">;
        
        lookFront();
        
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (e.type == "mouseout"<span style="color: #000000;">) {
        
        lookFront();
        
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (e.type == "contextmenu"<span style="color: #000000;">) {
        
        changeModel();
    }

}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> touchEvent(e)
{
    e.preventDefault();
    
    </span><span style="color: #0000ff;">var</span> touch = e.touches[0<span style="color: #000000;">];
    
    </span><span style="color: #0000ff;">if</span> (e.type == "touchstart"<span style="color: #000000;">) {
        </span><span style="color: #0000ff;">if</span> (e.touches.length == 1<span style="color: #000000;">) modelTurnHead(touch);
        </span><span style="color: #008000;">//</span><span style="color: #008000;"> onClick(touch);</span>
<span style="color: #000000;">        
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (e.type == "touchmove"<span style="color: #000000;">) {
        followPointer(touch);
        
        </span><span style="color: #0000ff;">if</span> (e.touches.length == 2<span style="color: #000000;">) {
            </span><span style="color: #0000ff;">var</span> touch1 = e.touches[0<span style="color: #000000;">];
            </span><span style="color: #0000ff;">var</span> touch2 = e.touches[1<span style="color: #000000;">];
            
            </span><span style="color: #0000ff;">var</span> len = Math.pow(touch1.pageX - touch2.pageX, 2) + Math.pow(touch1.pageY - touch2.pageY, 2<span style="color: #000000;">);
            </span><span style="color: #0000ff;">if</span> (thisRef.oldLen - len &lt; 0) modelScaling(1.025<span style="color: #000000;">); 
            </span><span style="color: #0000ff;">else</span> modelScaling(0.975<span style="color: #000000;">); 
            
            thisRef.oldLen </span>=<span style="color: #000000;"> len;
        }
        
    } </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (e.type == "touchend"<span style="color: #000000;">) {
        lookFront();
    }
}




</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> transformViewX(deviceX)
{
    </span><span style="color: #0000ff;">var</span> screenX = <span style="color: #0000ff;">this</span><span style="color: #000000;">.deviceToScreen.transformX(deviceX); 
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> viewMatrix.invertTransformX(screenX); 
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> transformViewY(deviceY)
{
    </span><span style="color: #0000ff;">var</span> screenY = <span style="color: #0000ff;">this</span><span style="color: #000000;">.deviceToScreen.transformY(deviceY); 
    </span><span style="color: #0000ff;">return</span><span style="color: #000000;"> viewMatrix.invertTransformY(screenY); 
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> transformScreenX(deviceX)
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.deviceToScreen.transformX(deviceX);
}


</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> transformScreenY(deviceY)
{
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">this</span><span style="color: #000000;">.deviceToScreen.transformY(deviceY);
}



</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> getWebGLContext()
{
    </span><span style="color: #0000ff;">var</span> NAMES = [ "webgl" , "experimental-webgl" , "webkit-3d" , "moz-webgl"<span style="color: #000000;">];
    
    </span><span style="color: #0000ff;">for</span>( <span style="color: #0000ff;">var</span> i = 0; i &lt; NAMES.length; i++<span style="color: #000000;"> ){
        </span><span style="color: #0000ff;">try</span><span style="color: #000000;">{
            </span><span style="color: #0000ff;">var</span> ctx = <span style="color: #0000ff;">this</span>.canvas.getContext(NAMES[i], {premultipliedAlpha : <span style="color: #0000ff;">true</span><span style="color: #000000;">});
            </span><span style="color: #0000ff;">if</span>(ctx) <span style="color: #0000ff;">return</span><span style="color: #000000;"> ctx;
        } 
        </span><span style="color: #0000ff;">catch</span><span style="color: #000000;">(e){}
    }
    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">null</span><span style="color: #000000;">;
};



</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> l2dLog(msg) {
    </span><span style="color: #0000ff;">if</span>(!LAppDefine.DEBUG_LOG) <span style="color: #0000ff;">return</span><span style="color: #000000;">;
    
   
    console.log(msg);
}



</span><span style="color: #0000ff;">function</span><span style="color: #000000;"> l2dError(msg)
{
    </span><span style="color: #0000ff;">if</span>(!LAppDefine.DEBUG_LOG) <span style="color: #0000ff;">return</span><span style="color: #000000;">;
    
    l2dLog( </span>"&lt;span style='color:red'&gt;" + msg + "&lt;/span&gt;"<span style="color: #000000;">);
    
    console.error(msg);
};</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>这时的index.html为</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;!</span><span style="color: #ff00ff;">DOCTYPE HTML</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>
     <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">='lib/live2d.min.js'</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">='framework/Live2DFramework.js'</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/utils/MatrixStack.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/utils/ModelSettingJson.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/PlatformManager.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/LAppDefine.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/LAppModel.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/LAppLive2DManager.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script </span><span style="color: #ff0000;">src</span><span style="color: #0000ff;">="src/SampleApp1.js"</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">head</span><span style="color: #0000ff;">&gt;</span>


<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">canvas </span><span style="color: #ff0000;">id</span><span style="color: #0000ff;">="glCanvas"</span><span style="color: #ff0000;"> width</span><span style="color: #0000ff;">="450px"</span><span style="color: #ff0000;"> height</span><span style="color: #0000ff;">="500px"</span><span style="color: #ff0000;"> style</span><span style="color: #0000ff;">="position:fixed;right:0px;bottom:-10px;"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">canvas</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span><span style="background-color: #f5f5f5; color: #000000;">
      SampleApp1();
    </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">script</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">body</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">html</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<p>&nbsp;这时的控制台已经有了我们想要的错误了</p>
<p>&nbsp;PlatformManager中</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160218234155847-880944210.png" alt="" width="1842" height="152" /></p>
<p>failed to load，所以我们就能知道我们的模型到底该导到哪去</p>
<p>这里要的是一个json，我看官方的文档写的json是定义的模型类，这里就直接试着改一下，去下载一个模型文件，看看都有些什么&hellip;&hellip;</p>
<p>下载到KcWiki曾经使用过的丛云模型，文件结构为</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160219121441956-246753187.png" alt="" width="290" height="380" /></p>
<p>model.json中内容为</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span>"version":"Sample 1.0.0"<span style="color: #000000;">,
    </span>"model":"murakumo.moc"<span style="color: #000000;">,
    </span>"textures"<span style="color: #000000;">:[
        </span>"murakumo.2048/texture_00.png"<span style="color: #000000;">
    ],
    </span>"motions"<span style="color: #000000;">:{
        </span>"tap_bust"<span style="color: #000000;">:[
            {</span>"file":"motions/murakumo_tap_bust_01.mtn"<span style="color: #000000;">},
            {</span>"file":"motions/murakumo_tap_bust_02.mtn"<span style="color: #000000;">}
        ],
        </span>"idle"<span style="color: #000000;">:[
            {</span>"file":"motions/murakumo_idle_01.mtn"<span style="color: #000000;">},
            {</span>"file":"motions/murakumo_idle_02.mtn"<span style="color: #000000;">},
            {</span>"file":"motions/murakumo_idle_03.mtn"<span style="color: #000000;">}
        ],
        </span>"tap_ear"<span style="color: #000000;">:[
            {</span>"file":"motions/murakumo_tap_ear_01.mtn"<span style="color: #000000;">}
        ],
        </span>"tap"<span style="color: #000000;">:[
            {</span>"file":"motions/murakumo_m_01.mtn"<span style="color: #000000;">},
            {</span>"file":"motions/murakumo_m_02.mtn"<span style="color: #000000;">}
        ]
    },
    </span>"physics":"murakumo.physics.json"<span style="color: #000000;">
}</span></pre>
</div>
<p>&nbsp;</p>
<p>所以我们能在这里看到&hellip;&hellip;版本，模型地址，资源动作和&hellip;&hellip;物理特性（讲道理我猜是乳摇用的&hellip;&hellip;</p>
<p>试着导入模型&hellip;&hellip;导入到哪？？</p>
<p>platform不是直接用到的，仔细看一看发现，</p>
<p>SampleApp1中有&nbsp;this.live2DMgr = new LAppLive2DManager();</p>
<p>而LppLive2DManager.js中，有function LAppLive2DManager()，其中有一句Live2DFramework.setPlatformManager(new PlatformManager);</p>
<p>那么Platform就是这样被初始化的，这样产生了模型载入错误，但是路径是在哪设置的&hellip;&hellip;</p>
<p>重新扫一眼文件结构就能发现，有个js叫LAppDefine，看之</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> LAppDefine =<span style="color: #000000;"> {
    
    
    DEBUG_LOG : </span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
    DEBUG_MOUSE_LOG : </span><span style="color: #0000ff;">false</span><span style="color: #000000;">, 
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> DEBUG_DRAW_HIT_AREA : false, </span>
    <span style="color: #008000;">//</span><span style="color: #008000;"> DEBUG_DRAW_ALPHA_MODEL : false, </span>
<span style="color: #000000;">    
    
    
    
    VIEW_MAX_SCALE : </span>2<span style="color: #000000;">,
    VIEW_MIN_SCALE : </span>0.8<span style="color: #000000;">,

    VIEW_LOGICAL_LEFT : </span>-1<span style="color: #000000;">,
    VIEW_LOGICAL_RIGHT : </span>1<span style="color: #000000;">,

    VIEW_LOGICAL_MAX_LEFT : </span>-2<span style="color: #000000;">,
    VIEW_LOGICAL_MAX_RIGHT : </span>2<span style="color: #000000;">,
    VIEW_LOGICAL_MAX_BOTTOM : </span>-2<span style="color: #000000;">,
    VIEW_LOGICAL_MAX_TOP : </span>2<span style="color: #000000;">,
    
    
    PRIORITY_NONE : </span>0<span style="color: #000000;">,
    PRIORITY_IDLE : </span>1<span style="color: #000000;">,
    PRIORITY_NORMAL : </span>2<span style="color: #000000;">,
    PRIORITY_FORCE : </span>3<span style="color: #000000;">,
    
    
    BACK_IMAGE_NAME : </span>"assets/image/back_class_normal.png"<span style="color: #000000;">,

    
    MODEL_HARU : </span>"assets/live2d/haru/haru.model.json"<span style="color: #000000;">,
    MODEL_HARU_A : </span>"assets/live2d/haru/haru_01.model.json"<span style="color: #000000;">,
    MODEL_HARU_B : </span>"assets/live2d/haru/haru_02.model.json"<span style="color: #000000;">,
    MODEL_SHIZUKU : </span>"assets/live2d/shizuku/shizuku.model.json"<span style="color: #000000;">,
    MODEL_WANKO : </span>"assets/live2d/wanko/wanko.model.json"<span style="color: #000000;">,
    
    
    MOTION_GROUP_IDLE : </span>"idle"<span style="color: #000000;">, 
    MOTION_GROUP_TAP_BODY : </span>"tap_body"<span style="color: #000000;">, 
    MOTION_GROUP_FLICK_HEAD : </span>"flick_head"<span style="color: #000000;">, 
    MOTION_GROUP_PINCH_IN : </span>"pinch_in"<span style="color: #000000;">, 
    MOTION_GROUP_PINCH_OUT : </span>"pinch_out"<span style="color: #000000;">, 
    MOTION_GROUP_SHAKE : </span>"shake"<span style="color: #000000;">, 

    
    HIT_AREA_HEAD : </span>"head"<span style="color: #000000;">,
    HIT_AREA_BODY : </span>"body"<span style="color: #000000;">
    
};</span></pre>
</div>
<p>&nbsp;</p>
<p>这地方大概绑了模型，和它的动作，这时候最好对比一下Sample模型的json</p>
<p>这是haru的json</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span>"type":"Live2D Model Setting"<span style="color: #000000;">,
    </span>"name":"haru"<span style="color: #000000;">,
    </span>"model":"haru_01.moc"<span style="color: #000000;">,
    </span>"textures"<span style="color: #000000;">:
    [
        </span>"haru_01.1024/texture_00.png"<span style="color: #000000;">,
        </span>"haru_01.1024/texture_01.png"<span style="color: #000000;">,
        </span>"haru_01.1024/texture_02.png"<span style="color: #000000;">
    ],
    </span>"physics":"haru.physics.json"<span style="color: #000000;">,
    </span>"pose":"haru.pose.json"<span style="color: #000000;">,
    </span>"expressions"<span style="color: #000000;">:
    [
        {</span>"name":"f01","file":"expressions/f01.exp.json"<span style="color: #000000;">},
        {</span>"name":"f02","file":"expressions/f02.exp.json"<span style="color: #000000;">},
        {</span>"name":"f03","file":"expressions/f03.exp.json"<span style="color: #000000;">},
        {</span>"name":"f04","file":"expressions/f04.exp.json"<span style="color: #000000;">},
        {</span>"name":"f05","file":"expressions/f05.exp.json"<span style="color: #000000;">},
        {</span>"name":"f06","file":"expressions/f06.exp.json"<span style="color: #000000;">},
        {</span>"name":"f07","file":"expressions/f07.exp.json"<span style="color: #000000;">},
        {</span>"name":"f08","file":"expressions/f08.exp.json"<span style="color: #000000;">}
    ],
    </span>"layout"<span style="color: #000000;">:
    {
        </span>"center_x":0<span style="color: #000000;">,
        </span>"y":1.2<span style="color: #000000;">,
        </span>"width":2.9<span style="color: #000000;">
    },
    </span>"hit_areas"<span style="color: #000000;">:
    [
        {</span>"name":"head", "id":"D_REF.HEAD"<span style="color: #000000;">},
        {</span>"name":"body", "id":"D_REF.BODY"<span style="color: #000000;">}
    ],
    </span>"motions"<span style="color: #000000;">:
    {
        </span>"idle"<span style="color: #000000;">:
        [
            {</span>"file":"motions/idle_00.mtn" ,"fade_in":2000, "fade_out":2000<span style="color: #000000;">},
            {</span>"file":"motions/idle_01.mtn" ,"fade_in":2000, "fade_out":2000<span style="color: #000000;">},
            {</span>"file":"motions/idle_02.mtn" ,"fade_in":2000, "fade_out":2000<span style="color: #000000;">}
        ],
        </span>"tap_body"<span style="color: #000000;">:
        [
            { </span>"file":"motions/tapBody_00.mtn" , "sound":"sounds/tapBody_00.mp3"<span style="color: #000000;">},
            { </span>"file":"motions/tapBody_01.mtn" , "sound":"sounds/tapBody_01.mp3"<span style="color: #000000;">},
            { </span>"file":"motions/tapBody_02.mtn" , "sound":"sounds/tapBody_02.mp3"<span style="color: #000000;">}
        ],
        </span>"pinch_in"<span style="color: #000000;">:
        [
            { </span>"file":"motions/pinchIn_00.mtn", "sound":"sounds/pinchIn_00.mp3"<span style="color: #000000;"> }
        ],
        </span>"pinch_out"<span style="color: #000000;">:
        [
            { </span>"file":"motions/pinchOut_00.mtn", "sound":"sounds/pinchOut_00.mp3"<span style="color: #000000;"> }
        ],
        </span>"shake"<span style="color: #000000;">:
        [
            { </span>"file":"motions/shake_00.mtn", "sound":"sounds/shake_00.mp3","fade_in":500<span style="color: #000000;"> }
        ],
        </span>"flick_head"<span style="color: #000000;">:
        [
            { </span>"file":"motions/flickHead_00.mtn", "sound":"sounds/flickHead_00.mp3"<span style="color: #000000;"> }
        ]
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>shizuku的json</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">{
    </span>"type":"Live2D Model Setting"<span style="color: #000000;">,
    </span>"name":"shizuku"<span style="color: #000000;">,
    </span>"model":"shizuku.moc"<span style="color: #000000;">,
    </span>"textures"<span style="color: #000000;">:
    [
        </span>"shizuku.1024/texture_00.png"<span style="color: #000000;">,
        </span>"shizuku.1024/texture_01.png"<span style="color: #000000;">,
        </span>"shizuku.1024/texture_02.png"<span style="color: #000000;">,
        </span>"shizuku.1024/texture_03.png"<span style="color: #000000;">,
        </span>"shizuku.1024/texture_04.png"<span style="color: #000000;">,
        </span>"shizuku.1024/texture_05.png"<span style="color: #000000;">
    ],
    </span>"physics":"shizuku.physics.json"<span style="color: #000000;">,
    </span>"pose":"shizuku.pose.json"<span style="color: #000000;">,
    </span>"expressions"<span style="color: #000000;">:
    [
     {</span>"name":"f01","file":"expressions/f01.exp.json"<span style="color: #000000;">},
     {</span>"name":"f02","file":"expressions/f02.exp.json"<span style="color: #000000;">},
     {</span>"name":"f03","file":"expressions/f03.exp.json"<span style="color: #000000;">},
     {</span>"name":"f04","file":"expressions/f04.exp.json"<span style="color: #000000;">}
    ],
    </span>"layout"<span style="color: #000000;">:
    {
        </span>"center_x":0<span style="color: #000000;">,
        </span>"y":1.2<span style="color: #000000;">,
        </span>"width":2.4<span style="color: #000000;">
    },
    </span>"hit_areas"<span style="color: #000000;">:
    [
        {</span>"name":"head", "id":"D_REF.HEAD"<span style="color: #000000;">},
        {</span>"name":"body", "id":"D_REF.BODY"<span style="color: #000000;">}
    ],
    </span>"motions"<span style="color: #000000;">:
    {
        </span>"idle"<span style="color: #000000;">:
        [
            {</span>"file":"motions/idle_00.mtn" ,"fade_in":2000, "fade_out":2000<span style="color: #000000;">},
            {</span>"file":"motions/idle_01.mtn" ,"fade_in":2000, "fade_out":2000<span style="color: #000000;">},
            {</span>"file":"motions/idle_02.mtn" ,"fade_in":2000, "fade_out":2000<span style="color: #000000;">}
        ],
        </span>"tap_body"<span style="color: #000000;">:
        [
            { </span>"file":"motions/tapBody_00.mtn", "sound":"sounds/tapBody_00.mp3"<span style="color: #000000;"> },
            { </span>"file":"motions/tapBody_01.mtn", "sound":"sounds/tapBody_01.mp3"<span style="color: #000000;"> },
            { </span>"file":"motions/tapBody_02.mtn", "sound":"sounds/tapBody_02.mp3"<span style="color: #000000;"> }
        ],
        </span>"pinch_in"<span style="color: #000000;">:
        [
            { </span>"file":"motions/pinchIn_00.mtn", "sound":"sounds/pinchIn_00.mp3"<span style="color: #000000;"> },
            { </span>"file":"motions/pinchIn_01.mtn", "sound":"sounds/pinchIn_01.mp3"<span style="color: #000000;"> },
            { </span>"file":"motions/pinchIn_02.mtn", "sound":"sounds/pinchIn_02.mp3"<span style="color: #000000;"> }
        ],
        </span>"pinch_out"<span style="color: #000000;">:
        [
            { </span>"file":"motions/pinchOut_00.mtn", "sound":"sounds/pinchOut_00.mp3"<span style="color: #000000;"> },
            { </span>"file":"motions/pinchOut_01.mtn", "sound":"sounds/pinchOut_01.mp3"<span style="color: #000000;"> },
            { </span>"file":"motions/pinchOut_02.mtn", "sound":"sounds/pinchOut_02.mp3"<span style="color: #000000;"> }
        ],
        </span>"shake"<span style="color: #000000;">:
        [
            { </span>"file":"motions/shake_00.mtn", "sound":"sounds/shake_00.mp3","fade_in":500<span style="color: #000000;"> },
            { </span>"file":"motions/shake_01.mtn", "sound":"sounds/shake_01.mp3","fade_in":500<span style="color: #000000;"> },
            { </span>"file":"motions/shake_02.mtn", "sound":"sounds/shake_02.mp3","fade_in":500<span style="color: #000000;"> }
        ],
        </span>"flick_head"<span style="color: #000000;">:
        [
            { </span>"file":"motions/flickHead_00.mtn", "sound":"sounds/flickHead_00.mp3"<span style="color: #000000;"> },
            { </span>"file":"motions/flickHead_01.mtn", "sound":"sounds/flickHead_01.mp3"<span style="color: #000000;"> },
            { </span>"file":"motions/flickHead_02.mtn", "sound":"sounds/flickHead_02.mp3"<span style="color: #000000;"> }
        ]
    }
}</span></pre>
</div>
<p>&nbsp;</p>
<p>motions大概都是对应的，根据上边贴了的丛云（murakumo）的json，试着把Define的js改为</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">var</span> LAppDefine =<span style="color: #000000;"> {
    
    
    DEBUG_LOG : </span><span style="color: #0000ff;">true</span><span style="color: #000000;">,
    DEBUG_MOUSE_LOG : </span><span style="color: #0000ff;">false</span><span style="color: #000000;">, 
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> DEBUG_DRAW_HIT_AREA : false, </span>
    <span style="color: #008000;">//</span><span style="color: #008000;"> DEBUG_DRAW_ALPHA_MODEL : false, </span>
<span style="color: #000000;">    
    
    
    
    VIEW_MAX_SCALE : </span>2<span style="color: #000000;">,
    VIEW_MIN_SCALE : </span>0.8<span style="color: #000000;">,

    VIEW_LOGICAL_LEFT : </span>-1<span style="color: #000000;">,
    VIEW_LOGICAL_RIGHT : </span>1<span style="color: #000000;">,

    VIEW_LOGICAL_MAX_LEFT : </span>-2<span style="color: #000000;">,
    VIEW_LOGICAL_MAX_RIGHT : </span>2<span style="color: #000000;">,
    VIEW_LOGICAL_MAX_BOTTOM : </span>-2<span style="color: #000000;">,
    VIEW_LOGICAL_MAX_TOP : </span>2<span style="color: #000000;">,
    
    
    PRIORITY_NONE : </span>0<span style="color: #000000;">,
    PRIORITY_IDLE : </span>1<span style="color: #000000;">,
    PRIORITY_NORMAL : </span>2<span style="color: #000000;">,
    PRIORITY_FORCE : </span>3<span style="color: #000000;">,
    
</span><span style="color: #008000;">/*</span><span style="color: #008000;">
    BACK_IMAGE_NAME : "assets/image/back_class_normal.png",

    
    MODEL_HARU : "assets/live2d/haru/haru.model.json",
    MODEL_HARU_A : "assets/live2d/haru/haru_01.model.json",
    MODEL_HARU_B : "assets/live2d/haru/haru_02.model.json",
    MODEL_SHIZUKU : "assets/live2d/shizuku/shizuku.model.json",
    MODEL_WANKO : "assets/live2d/wanko/wanko.model.json",
    
    
    MOTION_GROUP_IDLE : "idle", 
    MOTION_GROUP_TAP_BODY : "tap_body", 
    MOTION_GROUP_FLICK_HEAD : "flick_head", 
    MOTION_GROUP_PINCH_IN : "pinch_in", 
    MOTION_GROUP_PINCH_OUT : "pinch_out", 
    MOTION_GROUP_SHAKE : "shake", 

    
    HIT_AREA_HEAD : "head",
    HIT_AREA_BODY : "body"
</span><span style="color: #008000;">*/</span><span style="color: #000000;">

    MODEL_MURAKUMO : </span>"murakumo/murakumo.model.json"<span style="color: #000000;">,
    
    
    MOTION_GROUP_IDLE : </span>"idle"<span style="color: #000000;">, 
    MOTION_GROUP_TAP : </span>"tap"<span style="color: #000000;">, 
    MOTION_GROUP_TAP_EAR : </span>"tap_ear"<span style="color: #000000;">, 
    MOTION_GROUP_TAP_BUST : </span>"tap_bust"<span style="color: #000000;">, 

    
    HIT_AREA_HEAD : </span>"head"<span style="color: #000000;">,
    HIT_AREA_BODY : </span>"body"<span style="color: #000000;">,
    HIT_AREA_EAR_L  : </span>"ear_l"<span style="color: #000000;">,
    HIT_AREA_EAR_R  : </span>"ear_r"<span style="color: #000000;">,
    HIT_AREA_BUST : </span>"bust"<span style="color: #000000;">
};</span></pre>
</div>
<p>&nbsp;</p>
<p>接着出现的新的错误：</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160219124048863-1215186613.png" alt="" width="1264" height="256" /></p>
<p>LAPPModel在Load时出了问题&hellip;&hellip;PATH不对，搜搜看哪里使用了它&hellip;&hellip;</p>
<p>LAppLive2DManager.prototype.changeModel 有使用，是因为Sample里官方包含了好多模型&hellip;&hellip;改之</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160219124943550-377944876.png" alt="" width="476" height="379" /></p>
<div class="cnblogs_code">
<pre>LAppLive2DManager.prototype.changeModel = <span style="color: #0000ff;">function</span><span style="color: #000000;">(gl)
{
    </span><span style="color: #008000;">//</span><span style="color: #008000;"> console.log("--&gt; LAppLive2DManager.update(gl)");</span>
    
    <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span><span style="color: #000000;">.reloadFlg)
    {
        
        </span><span style="color: #0000ff;">this</span>.reloadFlg = <span style="color: #0000ff;">false</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">var</span> no = parseInt(<span style="color: #0000ff;">this</span>.count % 4<span style="color: #000000;">);

        </span><span style="color: #0000ff;">var</span> thisRef = <span style="color: #0000ff;">this</span><span style="color: #000000;">;
        </span><span style="color: #0000ff;">switch</span><span style="color: #000000;"> (no)
        {
            </span><span style="color: #0000ff;">case</span> 0<span style="color: #000000;">: 
                </span><span style="color: #0000ff;">this</span>.releaseModel(1<span style="color: #000000;">, gl);
                </span><span style="color: #0000ff;">this</span>.releaseModel(0<span style="color: #000000;">, gl);
                </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.createModel();
                </span><span style="color: #0000ff;">this</span>.models[0<span style="color: #000000;">].load(gl, LAppDefine.MODEL_MURAKUMO);
                </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
                </span><span style="color: #008000;">/*</span><span style="color: #008000;">
            case 1: 
                this.releaseModel(0, gl);
                this.createModel();
                this.models[0].load(gl, LAppDefine.MODEL_SHIZUKU);
                break;
            case 2: 
                this.releaseModel(0, gl);
                this.createModel();
                this.models[0].load(gl, LAppDefine.MODEL_WANKO);            
                break;
            case 3: 
                this.releaseModel(0, gl);
                
                // 一体目のモデル
                this.createModel();
                this.models[0].load(gl, LAppDefine.MODEL_HARU_A, function() {
                    // 二体目のモデル
                    thisRef.createModel();
                    thisRef.models[1].load(gl, LAppDefine.MODEL_HARU_B);
                });
                
                break;
                </span><span style="color: #008000;">*/</span>
            <span style="color: #0000ff;">default</span><span style="color: #000000;">:
                </span><span style="color: #0000ff;">break</span><span style="color: #000000;">;
        }
    }
};</span></pre>
</div>
<p>&nbsp;</p>
<p>然后再刷新&hellip;&hellip;看看啥错误</p>
<p>&nbsp;</p>
<p>卧槽！</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160219125300644-1787862754.png" alt="" width="477" height="450" /></p>
<p>野生的丛云出现了</p>
<p>测试一下motions&hellip;&hellip;无效</p>
<p>点击没有给出反应，并且点击耳朵应该会有特殊动作（json中的说明）</p>
<p>想来也是，不同的模型有不同的motion，只对json进行了绑定，具体运行好像没有写/改过，应该还漏了某些地方&hellip;&hellip;</p>
<p>试着去搜一下最开始json中绑定的motion变量，能搜到同样LAPPLive2DManager中，有</p>
<div class="cnblogs_code">
<pre>LAppLive2DManager.prototype.tapEvent = <span style="color: #0000ff;">function</span><span style="color: #000000;">(x, y)
{    
    </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_LOG)
        console.log(</span>"tapEvent view x:" + x + " y:" +<span style="color: #000000;"> y);

    </span><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">var</span> i = 0; i &lt; <span style="color: #0000ff;">this</span>.models.length; i++<span style="color: #000000;">)
    {

        </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].hitTest(LAppDefine.HIT_AREA_HEAD, x, y))
        {
            
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_LOG)
                console.log(</span>"Tap face."<span style="color: #000000;">);

            </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].setRandomExpression();
        }
        </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].hitTest(LAppDefine.HIT_AREA_BODY, x, y))
        {
            
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_LOG)
                console.log(</span>"Tap body." + " models[" + i + "]"<span style="color: #000000;">);

            </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].startRandomMotion(LAppDefine.MOTION_GROUP_TAP_BODY,
                                             LAppDefine.PRIORITY_NORMAL);
        }
    }

    </span><span style="color: #0000ff;">return</span> <span style="color: #0000ff;">true</span><span style="color: #000000;">;
};</span></pre>
</div>
<p>&nbsp;</p>
<p>所以可以根据murakumo的json来改一下这个函数</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">for</span> (<span style="color: #0000ff;">var</span> i = 0; i &lt; <span style="color: #0000ff;">this</span>.models.length; i++<span style="color: #000000;">)
    {

        </span><span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].hitTest(LAppDefine.HIT_AREA_HEAD, x, y))
        {
            
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_LOG)
                console.log(</span>"Tap face."<span style="color: #000000;">);

            </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].startRandomMotion(LAppDefine.MOTION_GROUP_TAP,
                                             LAppDefine.PRIORITY_NORMAL);
        }
        </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].hitTest(LAppDefine.HIT_AREA_EAR_L, x, y))
        {
            
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_LOG)
                console.log(</span>"Tap body." + " models[" + i + "]"<span style="color: #000000;">);

            </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].startRandomMotion(LAppDefine.MOTION_GROUP_TAP_EAR,
                                             LAppDefine.PRIORITY_NORMAL);
        }
        </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].hitTest(LAppDefine.HIT_AREA_EAR_R, x, y))
        {
            
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_LOG)
                console.log(</span>"Tap body." + " models[" + i + "]"<span style="color: #000000;">);

            </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].startRandomMotion(LAppDefine.MOTION_GROUP_TAP_EAR,
                                             LAppDefine.PRIORITY_NORMAL);
        }
        </span><span style="color: #0000ff;">else</span> <span style="color: #0000ff;">if</span> (<span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].hitTest(LAppDefine.HIT_AREA_BUST, x, y))
        {
            
            </span><span style="color: #0000ff;">if</span><span style="color: #000000;"> (LAppDefine.DEBUG_LOG)
                console.log(</span>"Tap body." + " models[" + i + "]"<span style="color: #000000;">);

            </span><span style="color: #0000ff;">this</span><span style="color: #000000;">.models[i].startRandomMotion(LAppDefine.MOTION_GROUP_TAP_BUST,
                                             LAppDefine.PRIORITY_NORMAL);
        }
    }</span></pre>
</div>
<p>&nbsp;</p>
<p>事实上改过以后控制台仍无输出</p>
<p>意思是点击事件还是没成功</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160219134247222-937751523.png" alt="" width="451" height="274" /></p>
<p>tapEvent报告了点击坐标，但是没有触发事件</p>
<p>而murakumo_idle是随机的表情动作，与点击事件是不同的，那么只能再跟踪一下tapEvent</p>
<p>tapEvent上来首先是打印坐标，有坐标打印出来说明函数是运行了</p>
<p>重新理一遍，经过前辈提醒，json数据被有绑定完全，再翻上去看看json</p>
<p>官方的sample里</p>
<p>除了textures，model，motion等等还有一个hit_areas，看来就是这样了</p>
<p>没有获取到hitareas，所以相当于没点上什么的</p>
<p>json中添加</p>
<div class="cnblogs_code">
<pre>"hit_areas"<span style="color: #000000;">:
    [
        {</span>"name":"head", "id":"D_REF.HEAD"<span style="color: #000000;">},
        {</span>"name":"body", "id":"D_REF.BODY"<span style="color: #000000;">},
        {</span>"name":"ear_l", "id":"D_REF.EAR_L"<span style="color: #000000;">},
        {</span>"name":"ear_r", "id":"D_REF.EAR_R"<span style="color: #000000;">},
        {</span>"name":"bust", "id":"D_REF.BUST"<span style="color: #000000;">}
    ],</span></pre>
</div>
<p>&nbsp;</p>
<p>至于这里的ID，是根据.moc模型文件获取的，是模型制作者在制作模型时为部位添加的，官方有提供模型编辑软件，或者记事本去开moc也能看到？</p>
<p>最后大功告成~</p>
<p><img src="http://images2015.cnblogs.com/blog/837926/201602/837926-20160219142225003-2080551982.png" alt="" width="1068" height="1008" /></p>
<p>&nbsp;</p>
