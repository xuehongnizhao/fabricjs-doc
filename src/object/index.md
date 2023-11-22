# Object
根object类，所有二维形状类都从该类继承

### 触发
- event:added
- event:removed
- event:selected
- event:deselected
- event:modified
- event:modified
- event:moved
- event:scaled
- event:rotated
- event:skewed
- event:rotating
- event:scaling
- event:moving
- event:skewing
- event:mousedown
- event:mouseup
- event:mouseover
- event:mouseout
- event:mousewheel
- event:mousedblclick
- event:dragover
- event:dragenter
- event:dragleave
- event:drop
### 成员
- (static) ***__uid*** :Number
  
创建 SVG 元素时内部使用的唯一 ID
- (static, constant) ***ENLIVEN_PROPS*** :Array.<string>
  
定义应从传递给 `fabric.Object._fromObject` 的object中激活哪些属性
- (static, constant) ***NUM_FRACTION_DIGITS*** :Number
  
定义object值序列化时使用的分数位数。您可以用它来提高/降低left、top、scaleX、scaleY 等值的精度。
- ***__corner*** :number|string|any

保留鼠标移动时最后悬停的角的值。0 表示无角，或表示 "mt"、"ml"、"mtr "等。它应该是私有的，但作为只读属性使用也无妨。
- ***absolutePositioned*** :boolean

如果为 true，剪辑路径的顶部和左侧将相对于canvas，不受object变换的影响。这将使剪辑路径相对于canvas，但只剪辑特定object。警告 这是测试版，该功能可能会更改或更名。
- ***aCoords***

在 Fabric.js 中，`aCoords` 是一个object，它描述了一个object在canvas上的四个主要角的绝对坐标。这四个角分别是：左上（tl）、右上（tr）、左下（bl）和右下（br）。每个角都是一个包含 `x` 和 `y` 的 `Fabric.Point` 实例。

这些坐标取决于以下属性：宽度（width）、高度（height）、水平缩放（scaleX）、垂直缩放（scaleY）、水平倾斜（skewX）、垂直倾斜（skewY）、角度（angle）、线宽（strokeWidth）、顶部（top）和左侧（left）。

这些坐标对于理解object在哪里非常有用。它们会随着 `oCoords` 而更新，但是在缩放或平移改变时，它们不需要更新。这些坐标会通过 `setCoords` 方法更新。你可以通过 `calcACoords` 方法在不更新的情况下计算它们。
- ***angle*** :Number
- ***backgroundColor*** :String
- ***borderColor*** :String
- ***borderDashArray*** :Array
- ***borderOpacityWhenMoving*** :Number

当object处于活动和移动状态时，object控制边界的不透明度
- ***borderScaleFactor*** :Number

object控制边框的缩放因子，数值越大，边框越厚。默认边框的缩放因子为 1，因此这基本上就是边框的厚度，因为边框本身是无法更改的。
- ***cacheProperties*** :Array

在 Fabric.js 中，`cacheProperties` 是一个数组，它包含了一组属性名。这些属性被认为是影响object缓存的关键属性。

当 `statefullCache` 选项开启（或处于懒加载模式），或者当你通过 `Object.set(key, value)` 单独设置object属性时，Fabric.js 会检查这些属性是否在 `cacheProperties` 列表中。

如果属性名在 `cacheProperties` 列表中，那么object会被标记为 "dirty"（脏的），并且在下一次渲染时会被刷新。这意味着，如果你修改了列表中的任何一个属性，Fabric.js 会知道需要在下一次渲染时更新object的缓存。

例如，`cacheProperties` 可能包含如下属性：

```javascript
cacheProperties: ['fill', 'stroke', 'strokeWidth', 'strokeDashArray', 'width', 'height', 'strokeLineCap', 'strokeLineJoin', 'strokeMiterLimit', 'fillRule', 'backgroundColor']
```

在这个例子中，如果你修改了object的 `fill`、`stroke`、`width` 等属性，object就会在下一次渲染时被刷新。

- ***centeredRotation*** :Boolean

为真时，此object在通过控件旋转时将使用中心点作为变换原点。向后不兼容说明：该属性取代了 "centerTransform"（布尔值）。
- ***centeredScaling*** :Boolean

为真时，此object在通过控件缩放时将使用中心点作为变换的原点。向后不兼容说明：该属性取代了 "centerTransform"（布尔值）。
- ***clipPath*** :fabric.Object

剪切路径可以被看作是一个遮罩，它定义了哪些部分的canvas是可见的，这个属性接受一个 Fabric object（如 `fabric.Circle` 或 `fabric.Polygon`），并将其用作剪切路径。
- ***colorProperties*** :Array

`colorProperties` 是一个数组，它包含了一组属性名。这些属性被认为是影响object颜色动画的关键属性。

当你通过 `Object.animate(key, value)` 单独设置object属性时，Fabric.js 会检查这些属性是否在 `colorProperties` 列表中。

如果属性名在 `colorProperties` 列表中，那么object的颜色动画就会被触发。这意味着，如果你修改了列表中的任何一个属性，Fabric.js 会知道需要在下一次渲染时更新object的颜色动画。

例如，`colorProperties` 可能包含如下属性：

```javascript
colorProperties: ['fill', 'stroke']
```

在这个例子中，如果你修改了object的 `fill` 或 `stroke` 属性，object的颜色动画就会被触发。
- ***controls***

自定义控件界面控件由 default_controls.js 添加
- ***cornerColor*** :String
- ***cornerDashArray*** :Array
- ***cornerSize*** :Number
- ***cornerStrokeColor*** :String

控制object边角的颜色（当object处于活动状态且透明边角为假时）
- ***cornerStyle*** :String

指定控件样式，"矩形 "或 "圆形
- ***dirty*** :Boolean

设置为 "true "时，object的缓存将在下一次渲染调用时重新渲染。这意味着，如果你修改了object的任何属性，并且 dirty 属性被设置为 true，那么 Fabric.js 会知道需要在下一次渲染时更新object的缓存。这可以帮助提高渲染性能，特别是当你的object有许多属性需要频繁更新时。 自 1.7.0 起 
- ***evented*** :Boolean

设置为 "false "时，object不能成为事件的目标。所有事件都会通过它传播。在 v1.3.4 中引入
- ***excludeFromExport*** :Boolean
- ***fill*** :String
- ***fillRule*** :String

用于填充object的填充规则，接受的值为非零，偶数 向后不兼容说明：在 v1.4.12 之前，该属性用于设置 `globalCompositeOperation`（请使用 `fabric.Object#globalCompositeOperation` 代替）。
- ***flipX*** :Boolean
- ***flipY*** :Boolean
- ***globalCompositeOperation*** :String

canvas使用的合成规则 `globalCompositeOperation`
- ***hasBorders*** :Boolean
- ***hasControls*** :Boolean
- ***height*** :Number
- ***hoverCursor*** :String
- ***includeDefaultValues*** :Boolean

`includeDefaultValues` 是一个布尔值属性。当其值为 `false` 时，object的默认值不会包含在其序列化中。这意味着，当你序列化一个object（例如，将其转换为 JSON 格式）时，如果 `includeDefaultValues` 属性被设置为 `false`，那么object的默认值将不会被包含在序列化结果中。这可以帮助减少序列化结果的大小，特别是当你的object有许多默认值与默认设置相同的属性时。
- ***inverted*** :boolean

`inverted` 是一个布尔值属性，只有当object被用作 `clipPath` 时才有意义。如果 `inverted` 为 `true`，`clipPath` 将使object剪切到 `clipPath` 的外部。这意味着，如果你设置了object的 `clipPath` 属性，并且 `inverted` 属性被设置为 `true`，那么object将会被剪切到 `clipPath` 定义的路径之外。这可以帮助你创建一些特殊的视觉效果，例如，你可以使用一个object来剪切另一个object，以创建一个 "镂空" 的效果
- ***left*** :Number

object的左侧位置。请注意，默认情况下这是相对于object左侧的位置。您可以通过设置 `originX={left/center/right}` 来更改。
- ***lineCoords***

用canvas元素坐标描述object的角位置，包括填充。使用 setCoords 设置和刷新。
- ***lockMovementX*** :Boolean
- ***lockMovementY*** :Boolean
- ***lockRotation*** :Boolean
- ***lockScalingFlip*** :Boolean
- ***lockScalingX*** :Boolean
- ***lockScalingY*** :Boolean
- ***lockSkewingX*** :Boolean
- ***lockSkewingY*** :Boolean
- ***matrixCache***

object全变换矩阵的存储空间
- ***minScaleLimit*** :Number
- ***moveCursor*** :String
- ***noScaleCache*** :Boolean

`noScaleCache` 是一个布尔值属性。当其值为 `true` 时，object在缩放过程中不会更新缓存。如果object被放大过多，图像会变得块状，然后在缩放结束时用正确的细节重新绘制。这个设置取决于性能和应用需求。自 1.7.0 版本开始，默认值为 `true`。这意味着，如果你在缩放一个object时，而且 `noScaleCache` 属性被设置为 `true`，那么 Fabric.js 会知道在下一次渲染时需要更新object的缓存。这可以帮助提高渲染性能，特别是当你的object需要频繁更新时。
- ***objectCaching*** :Boolean

true "时，object会缓存在额外的canvas上。false "时，除非有必要，否则不会缓存object（clipPath） 默认为 true
- ***originX*** :String

`oCoords` 是一个object，它描述了一个object在canvas元素坐标中的四个主要角的位置。这四个角分别是：左上（tl）、右上（tr）、左下（bl）和右下（br）。每个角都是一个包含 `x`、`y` 和 `corner` 的object。`corner` 属性以类似的方式包含了角的交互区域的四个点。

`oCoords` 和 `aCoords` 都是描述object在canvas上四个主要角的位置的object，但它们的用途和计算方式有所不同。

 `oCoords`：这些坐标取决于控制的 `positionHandler`，并用于绘制和定位控制。当你移动、旋转或缩放一个object时，Fabric.js 会更新这些坐标，以便正确地绘制和定位object的控制。

 `aCoords`：这些坐标取决于以下属性：宽度（width）、高度（height）、水平缩放（scaleX）、垂直缩放（scaleY）、水平倾斜（skewX）、垂直倾斜（skewY）、角度（angle）、线宽（strokeWidth）、顶部（top）和左侧（left）。这些坐标用于object检测，并通过 `setCoords` 方法设置和刷新。当你移动、旋转或缩放一个object时，Fabric.js 会更新这些坐标，以便正确地检测和处理object。

你应该根据你的具体需求来选择使用哪一个。如果你需要绘制和定位object的控制，那么你应该使用 `oCoords`。如果你需要进行object检测，那么你应该使用 `aCoords`。

这些坐标取决于控制的 `positionHandler`，并用于绘制和定位控制。这意味着，当你移动、旋转或缩放一个object时，Fabric.js 会更新这些坐标，以便正确地绘制和定位object的控制。
- ***opacity*** :Number
- ***originX*** :String  ***originY*** :String

`originX` 是一个字符串属性，表示object的水平变换原点，可以是 "left"（左）、"right"（右）或 "center"（中）。这个属性决定了object在进行旋转或缩放时的基准点。例如，如果 `originX` 设置为 "left"，那么object将会围绕其左边缘进行旋转或缩放。同样，如果 `originX` 设置为 "center"，那么object将会围绕其中心进行旋转或缩放。你可以参考这个 [示例](http://fabricjs.com/test/misc/origin.html) 来了解 `originX`/`originY` 如何影响组中的object。 

- ***ownMatrixCache***

object变换矩阵存储

- ***padding*** :Number
- ***paintFirst*** :String

确定是先绘制填充还是先绘制描边（"填充 "或 "描边 "之一）
- ***perPixelTargetFind*** :Boolean

`perPixelTargetFind` 是一个布尔值属性。当其值被设置为 `true` 时，object在canvas上是通过每个像素点来查找的，而不是通过边界框。这意味着，如果你点击或拖动object，Fabric.js 会检查你点击或拖动的是object的哪个像素点，而不是检查你点击或拖动的是object的哪个边界框。这可以帮助提高object查找的精确度，特别是当你的object有复杂的形状或透明区域时。
(6) undefined. https://media.geeksforgeeks.org/wp-content/uploads/20200327230544/g4gicon.png.
- ***scaleX*** :Number
- ***scaleY*** :Number
- ***selectable*** :Boolean

如果设置为 "false"，则无法选择object进行修改（使用基于点的单击选择或基于组的选择）。但事件仍会触发。
- ***selectionBackgroundColor*** :String

选择object的背景色。当object处于活动状态时，object后面的彩色图层与 `globalCompositeOperation` 方法不兼容。
- ***shadow*** :fabric.Shadow

阴影object，代表此形状的阴影
- ***skewX*** :Number

物体 X 轴的倾斜角度（度数）
- ***skewY*** :Number

物体在 Y 轴上的倾斜角度（单位：度）
- ***statefullCache*** :Boolean

为 "true "时，object属性会在缓存无效时被检查。在某些特殊情况下，您可能希望禁用此功能（喷刷、非常大的组），或者如果您的应用程序不允许您修改组的属性，您希望禁用组的此功能。 自 1.7.0 起默认为 false
- ***stateProperties*** :Array

`stateProperties` 是一个数组，它包含了一组属性名。这些属性被认为是影响object状态改变的关键属性。

当你检查一个object的状态是否已经改变（使用 `fabric.Object#hasStateChanged` 方法）或者进行历史记录（如撤销/重做）时，Fabric.js 会检查这些属性是否在 `stateProperties` 列表中。

如果属性名在 `stateProperties` 列表中，那么object的状态就被认为已经改变。这可以帮助你跟踪object的状态，并在需要时进行相应的操作，如撤销或重做。

例如，`stateProperties` 可能包含如下属性：

```javascript
stateProperties: ['left', 'top', 'width', 'height', 'fill', 'stroke']
```

在这个例子中，如果你修改了object的 `left`、`top`、`width`、`height`、`fill` 或 `stroke` 属性，object的状态就被认为已经改变。
- ***stroke*** :String
- ***strokeDashArray*** :Array
- ***strokeDashOffset*** :Number
- ***strokeLineCap*** :String
- ***strokeLineJoin*** :String
- ***strokeMiterLimit*** :Number
- ***strokeUniform*** :Boolean

false "时，描边宽度将随object缩放。此属性不适用于文本类或使用 strokeText、fillText 方法的绘图调用。
- ***strokeWidth*** :Number
- ***top*** :Number
- ***touchCornerSize*** :Number

检测到触摸交互时object控制角的大小
- ***type*** :String

object类型（rect、circle、path等）。请注意，此属性为只读属性，不可修改。如果修改，Fabric 的某些部分（如 JSON 加载）将无法正常工作。
- ***visible*** :Boolean
- ***width*** :Number

### 方法

- ***_calcRotateMatrix()*** → {Array}

返回值
object的旋转矩阵
- ***_calcTranslateMatrix()*** → {Array}

返回值
object的旋转矩阵
- ***_drawClipPath(ctx, clipPath)***
准备 clipPath 状态和缓存，并将其绘制到实例的缓存中

- ***_getCoords(absolute)*** → {Object}

返回交集的正确坐标集，将返回 aCoords 或 lineCoords。

- ***_limitCacheSize(dims)*** → {Object|Object|Object|Object}

限制缓存尺寸，使 X * Y 不超过 `fabric.perfLimitSizeTotal`，每边不超过 `fabric.cacheSideLimit`，这些数字都是可配置的，这样就能获得尽可能多的细节，从而在性能上讨价还价。

- ***_removeCacheCanvas()***
- ***_renderControls(ctx, styleOverrideopt)***
- ***_setupCompositeOperation(ctx)***

设置特定object的canvas `globalCompositeOperation` 可使用 `globalCompositeOperation` 属性指定特定object的自定义合成操作
- ***adjustPosition(to)*** 
- ***animate(property, value)*** → {fabric.Object|fabric.AnimationContext|Array.<fabric.AnimationContext>}
- ***bringForward(intersectingopt)*** → {fabric.Object}
- ***bringToFront()*** → {fabric.Object}
- ***calcOwnMatrix()*** → {Array}

计算变换矩阵，表示object属性的当前变换，该矩阵不包括组变换
- ***calcTransformMatrix(skipGroupopt)*** → {Array}

计算变换矩阵，该矩阵表示object属性的当前变换。
- ***center()*** → {fabric.Object}
将object垂直和水平居中到上次添加object的canvas上。居中后可能需要调用object上的 `setCoords` 来更新控制区域。

- ***centerH()*** → {fabric.Object}
- ***centerV()*** → {fabric.Object}
- ***clone(callback, propertiesToIncludeopt)***
- ***cloneAsImage(callback, optionsopt)*** → {fabric.Object}

该方法可以将一个object转换为 Fabric.js 的 Image 实例。这个方法主要利用了 `toCanvasElement` 方法。在早期，这个方法是基于 `toDataUrl` 和 `loadImage` 方法的，所以它也有质量和格式选项。但是，`toCanvasElement` 方法更快，且不会损失质量。如果你需要从一个object中获取真正的 Jpeg 或 Png，使用 `toDataURL` 方法是正确的方式。`toCanvasElement` 方法和从得到的canvas中的 `toBlob` 方法也是一个好的选择。现在，这个方法是同步的，但仍然支持回调，因为我们不想打破它。当 Fabric.js 5.0 计划时，这可能会被改变，不再有回调。
- ***complexity()*** → {Number}

返回实例的复杂度
- ***containsPoint(point, linesopt, absoluteopt, calculateopt)*** → {Boolean}
- ***dispose()***

取消实例的运行动画
- ***drawBorders(ctx, styleOverride)*** → {fabric.Object}

绘制object边框的边界。需要公共属性：宽度、高度 需要公共选项：padding、borderColor
- ***drawBordersInGroup(ctx, options, styleOverride)*** → {fabric.Object}
- ***drawCacheOnCanvas(ctx)***
- ***drawClipPathOnCache(ctx, clipPath)***
- ***drawControls(ctx, styleOverride)*** → {fabric.Object}
- ***drawObject(ctx)***
- ***drawSelectionBackground(ctx)*** → {fabric.Object}
- ***forEachControl(fn)***
- ***fxStraighten(callbacks)*** → {fabric.Object}

和`fabric.Object.prototype.straighten`类似 但是有动画
- ***getBoundingRect(absoluteopt, calculateopt)*** → {Object}

返回object边界矩形（左、上、宽、高）的坐标，该矩形框与canvas轴线对齐。
- ***getCenterPoint()*** → {fabric.Point}
- ***getCoords()*** → {Array}
- ***getLocalPointer(e, pointeropt)*** → {Object}

返回鼠标指针相对于对象的坐标
- ***getObjectOpacity()*** → {Number}
- ***getObjectScaling()*** → {Object}
- ***getPointByOrigin(originX, originY)*** → {fabric.Point}
- ***getScaledHeight()*** → {Number}
- ***getScaledWidth()*** → {Number}
- ***getSvgCommons()*** → {String}
- ***getSvgFilter()*** → {String}
- ***getSvgSpanStyles(style, useWhiteSpace)*** → {String}
- ***getSvgStyles(skipShadow)*** → {String}
- ***getSvgTextDecoration(style)*** → {String}
- ***getSvgTransform(use)*** → {String}
- ***getTotalObjectScaling()*** → {Object}
- ***getViewportTransform()*** → {Array}
- ***hasFill()***
- ***hasStateChanged(propertySetopt)*** → {Boolean}
- ***hasStroke()***
- ***initialize(optionsopt)***
- ***intersectsWithObject(other, absoluteopt, calculateopt)*** → {Boolean}
- ***intersectsWithRect(pointTL, pointBR, absoluteopt, calculateopt)*** → {Boolean}
- ***isCacheDirty(skipCanvas)***
- ***isContainedWithinObject(other, absoluteopt, calculateopt) → {Boolean}***
- ***isContainedWithinRect(pointTL, pointBR, absoluteopt, calculateopt) → {Boolean}***
- ***isControlVisible(controlKey)*** → {Boolean}
- ***isOnScreen(calculateopt)*** → {Boolean}
- ***isPartiallyOnScreen(calculateopt)*** → {Boolean}
- ***isType(type)*** → {Boolean}
- ***moveTo(index)*** → {fabric.Object}
- ***needsItsOwnCache()***
- ***onDeselect(optionsopt)***
- ***onSelect(optionsopt)***
- ***render(ctx)***
- ***rotate(angle)*** → {fabric.Object}
- ***saveState(optionsopt)*** → {fabric.Object}
- ***scale(value)*** → {fabric.Object}
- ***scaleToHeight(value, absolute)*** → {fabric.Object}
- ***scaleToWidth(value, absolute)*** → {fabric.Object}
- ***sendBackwards(intersectingopt)*** → {fabric.Object}
- ***sendToBack()*** → {fabric.Object}
- ***setControlsVisibility(optionsopt)*** → {fabric.Object}
- ***setControlVisible(controlKey, visible)*** → {fabric.Object}
- ***setCoords(skipCornersopt)*** → {fabric.Object}
- ***setOnGroup()***
  
setOnGroup() 是 Fabric.js 中的一个回调函数。每当对象的父组中的非委托属性发生变化时，都会调用此函数。它会传入键和值作为参数。这个函数的主要作用是在组内的对象属性发生变化时进行一些特定的操作或处理。
- ***setOptions(optionsopt)***
- ***setPositionByOrigin(pos, originX, originY)*** → {void}
- ***setupState(optionsopt)*** → {fabric.Object}
- ***shouldCache()*** → {Boolean}
- ***straighten()*** → {fabric.Object}
- ***toCanvasElement(options)*** → {HTMLCanvasElement}
- ***toClipPathSVG(reviveropt)*** → {String}
- ***toDatalessObject(propertiesToIncludeopt)*** → {Object}
- ***toDataURL(options)*** → {String}
- ***toJSON(propertiesToIncludeopt)*** → {Object}
- ***toLocalPoint(point, originX, originY)*** → {fabric.Point}

“local” 通常指的是相对于当前 Fabric 对象的坐标系。例如，toLocalPoint(point, originX, originY) 方法会将一个全局坐标点转换为相对于当前对象的局部坐标点。
- ***toObject(propertiesToIncludeopt)*** → {Object}
- ***toString()*** → {String}
- ***toSVG(reviveropt)*** → {String}
- ***transform(ctx)***
- ***translateToCenterPoint(point, originX, originY)*** → {fabric.Point}

`translateToCenterPoint(point, originX, originY)` 是 Fabric.js 中的一个方法。这个方法将坐标从原点转换为中心坐标（基于对象的尺寸）。`point` 参数是一个点，`originX` 和 `originY` 参数分别是原点的 x 和 y 坐标。这个方法通常用于将坐标从一个原点转换为另一个原点
- ***translateToGivenOrigin(point, fromOriginX, fromOriginY, toOriginX, toOriginY)*** → {fabric.Point}
- ***translateToOriginPoint(center, originX, originY)*** → {fabric.Point}
- ***viewportCenter()*** → {fabric.Object}

`viewportCenter()` 是 Fabric.js 中的一个方法。这个方法会将对象在最后添加的画布的当前视口上居中。你可能需要在居中后调用 `setCoords` 方法来更新控制区域。
- ***viewportCenterH()*** → {fabric.Object}
- ***viewportCenterV()*** → {fabric.Object}
- ***willDrawShadow()*** → {Boolean}