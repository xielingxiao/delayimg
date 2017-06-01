# delayimg
移动端图片延迟加载，滚动到当前区域停留指定时间载入图片（包括背景图片、图片标签），可选容器


内置方法

1、delayimg.init()方法 初始化，可配置参数：

    content 加载区域外容器，值为dom对象，默认为window   如delayimg.init({content:document.getElementById('Content')});
    
    throttle  图片出现在可视区域throttle时间加载图片，默认为300毫秒
    
    offset  图片距离出现在可视区域offset加载图片，默认为零，即出现才添加至加载队列
    
    
2、delayimg.render()方法   追加图片方法，动态添加图片


html配置

图片标签对象使用 data-delay 属性存放真实图片地址，背景图片对象使用 data-delay-background 属性存放真实背景图片地址，两种形式对象可随意混用；

图片标签对象可以设置图片初始占位高度 如height='100'，透明度渐变请自行使用css transition: opacity .4s 灵活控制，js只会动态修改对象opatity为1，父级背景修改为transparent，移除占位高度height；


示例代码：

    ---------javascript---------
    
    $.ajax( {
        type: 'get',
        url: '..',
        data: {},
        dataType: 'json',
        cache: false,
        async: false,
        success: function ( data ){
            document.getElementById('Content').innerHTML='<img src='blank.gif' data-delay="data.imgSrc"/>'+
            '<b data-delay-background="data.imgBgSrc"></b>';
            delayimg.init({content:document.getElementById('Content')})
        }
    });
    
    el.addEventListener('tap',function(){
        document.getElementById('Content').insertAdjacentHTML('beforeend',
        '<img src="blank.gif" data-delay="data.imgSrc"/>');
        delayimg.render();
    });
    
    ------ css ------
    img{opacity: 0;transition: opacity .4s ease-in; }
    img--parentNode{ background:url || color} 背景图片同理，css可自行灵活设置
    

此js不基于任何框架，只是个简单方便的图片延迟加载小方法，主要针对与移动端，如有不足，欢迎补充


    
