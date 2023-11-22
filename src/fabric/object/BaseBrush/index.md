# BaseBrush 
# 成员
- ***color*** :String
- ***limitedToCanvasSize*** :Boolean

true时，自由绘图会限制在白板大小范围内。默认为 false。
- ***shadow*** :fabric.Shadow

代表此形状阴影的阴影对象。向后不兼容说明：自 v1.2.12 起，该属性取代了 "shadowColor"（字符串）、"shadowOffsetX"（数值）、"shadowOffsetY"（数值）和 "shadowBlur"（数值）。
- ***strokeDashArray*** :Array
- ***strokeLineCap*** :String

笔刷的线尾样式（"对接"、"圆形"、"方形"中的一种）"butt", "round", "square"
- ***strokeLineJoin*** :String

刷角样式（"斜角"、"圆形"、"斜切 "中的一种）"bevel", "round", "miter"
- ***strokeMiterLimit*** :Number 

笔刷的最大斜切长度（用于 strokeLineJoin = "miter"）。
- ***width*** :Number