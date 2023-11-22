# fabric
# 类
- ActiveSelection
- BaseBrush
- Canvas
- Circle
- CircleBrush
- Color
- Ellipse
- Gradient
- Group
- Image
- Intersection
- IText
- Line
- Object
- Path
- Pattern
- PatternBrush
- PencilBrush
- Point
- Polygon
- Polyline
- Rect
- Shadow
- SprayBrush
- StaticCanvas
- Text
- Textbox
- Triangle
  
# 命名空间

- Collection
- CommonMethods
- Observable
- util

# 成员

- (static) ***arcToSegmentsCache*** 

此对象包含弧线到贝塞尔曲线的转换结果，以便在需要再次转换同一弧线时更快地检索。它是一个内部变量，从 2.3.4 版开始可以访问。
- (static) ***boundsOfCurveCache*** 

该对象保留了由计算所需的连接参数映射的曲线边界计算结果。如果您解析和添加的路径总是相同的，那么它确实可以加快计算速度，但如果您大量使用自由绘制，那么计算速度就会大打折扣，而且内存中的对象也会变大。该对象以前是一个私有变量，现在被附加到程序库中，这样你就可以访问它，并最终清除它。这是一个内部变量，从 2.3.4 版开始可以访问

- (static) ***browserShadowBlurConstant*** :Number

特定于浏览器的常量，用于调整 CanvasRenderingContext2D.shadowBlur 值，该值没有单位，在不同浏览器中的呈现效果也不一样。效果不错的值（截至 2017 年 10 月）有- Chrome: 1.5 - Edge: 1.75 - Firefox：0.9 - Safari0.95

- (static) ***cachesBoundsOfCurve*** 

如果禁用，则不会使用 `boundsOfCurveCache`。对于大量使用铅笔绘制的应用程序来说，禁用它可能更好一些
- (static) ***charWidthsCache*** 

文本渲染中字符宽度的缓存对象。
- (static) ***devicePixelRatio*** 

`devicePixelRatio` 是一个静态属性，表示设备的像素比率。这个比率是设备物理像素和设备独立像素（DIPs）之间的比率。例如，高分辨率的设备（如 Retina 显示屏）的 `devicePixelRatio` 值通常大于 1。这个属性在处理设备的显示和图形渲染时非常有用，可以帮助确保图像和其他图形元素在所有设备上都能正确地渲染和显示。
- (static) ***disableStyleCopyPaste*** :Boolean

为'true'时，复制/粘贴文本时不保留样式信息，使粘贴的文本使用目标样式。默认为 "false"。
- (static) ***DPI*** 

每英寸像素默认设置为 96。可以更改，以实现更逼真的转换。
- (static) ***enableGLFiltering*** :Boolean

启用 Webgl 过滤图片（可用） 将初始化过滤后端，这将占用内存和时间，因为将为 gl 上下文创建默认的 2048x2048 画布
- (static) ***forceGLPutImageData*** :Boolean
- (static)  ***isLikelyNode*** :Boolean

当所处环境可能是 Node.js 时为 true
- (static) ***isTouchSupported*** :boolean
- (static) ***log***
  
console.log"（可用时）的封装程序
- (static) ***maxCacheSideLimit*** :Number

缓存画布宽度或高度的像素限制。IE 将最大值固定为 5000
- (static) ***minCacheSideLimit*** :Number
- (static) ***perfLimitSizeTotal*** :Number

缓存画布的像素限制。1Mpx、4Mpx 应该没问题。
- (static) ***RUNNING_ANIMATIONS*** :Array.`<AnimationContext>`

保存所有运行动画的数组
- (static) ***SHARED_ATTRIBUTES*** :array

从所有 SVG 元素中解析出的属性
- (static) ***textureSize*** :Number

如果启用了 Webgl 并可用，textureSize 将决定画布后台的大小
- (static) ***warn***

console.warn`（可用时）的包装器
# 方法
- (static) ***getCSSRules(doc)*** → {Object}

返回给定 SVG 文档的 CSS 规则
- (static) ***getGradientDefs(doc)*** → {Object}

解析 SVG 文档，返回其中的所有渐变声明
- (static) ***isWebglSupported(tileSize)*** → {Boolean}

说明用户浏览器是否支持该过滤后端。
- (static) ***loadSVGFromString(string, callback, reviveropt, optionsopt)***

获取与 SVG 文档相对应的字符串，并将其解析为一组fabric对象
- (static) ***loadSVGFromURL(url, callback, reviveropt, optionsopt)***
- (static) ***parseAttributes(element, attributes)*** → {Object}

根据给定的元素和属性名数组，返回属性名/值对象；向上递归解析父节点 "g"。
- (static) ***parseElements(elements, callback, optionsopt, reviveropt)***

将 svg 元素数组转换为相应的 fabric.* 实例
- (static) ***parseFontDeclaration(value, oStyle)***

解析简短的字体声明，并将其属性添加到样式对象中
- (static) ***parsePointsAttribute(points)*** → {Array}

解析 "point"属性，返回值数组
- (static) ***parseStyleAttribute(element)*** → {Object}

解析 "style "属性，返回一个包含值的对象
- (static) ***parseSVGDocument(doc, callback, reviveropt, parsingOptionsopt)***

解析 SVG 文档，将其转换为相应 fabric.* 实例的数组，并将其传递给回调函数
- (static) ***parseTransformAttribute(attributeValue)*** → {Array}

解析 "transform "属性，返回值数组