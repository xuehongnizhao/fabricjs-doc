# 使用transform，Fabric.js 简介第 6 部分
在前面的系列文章中，我们已经介绍了很多主题；从基本的对象操作到动画、事件、过滤器、组和子类。但还有一些非常有趣和有用的东西需要讨论！

了解transform如何在 fabricJS 上工作是尽可能顺利地编写应用程序的一个关键方面。

### 与transform相关的方法和属性
如果你打算理解并使用 fabricJS 变换来编写自定义代码，那么这些方法是你最应该学习使用的。
一般来说，在本页中，我们将matrix称为由 6 个数字组成的数组，表示平面上的变换；将point称为简单的 JS 对象，看起来像 `{ x: number, y: number }`，或者 `fabric.Point` 类实例。

Canvas:
- viewportTransform = matrix;

Objects:
- matrix = fabric.Object.prototype.calcTransformMatrix();
- matrix = fabric.Object.prototype.calcOwnMatrix();
 
Utils:
- point = fabric.util.transformPoint(point, matrix);
- matrix = fabric.util.multiplyTransformMatrices(matrix, matrix);
- matrix = fabric.util.invertTransform(matrix);
- options = fabric.util.qrDecompose(matrix);

### 从一个空间移动到另一个空间
使用 FabricJS 时，您经常需要与坐标和位置进行交互，但如果没有正确的背景知识，理解这些坐标的位置可能会很麻烦。
下面我将列出变换及其用法，然后试着举两个例子，以便更好地说明发生了什么以及如何操作。

`Canvas.viewportTransform`：将虚拟canvas上的一点移动到缩放和平移空间。
在应用 `viewportTransfrom M` 表示的缩放和平移后，canvas未缩放和平移时位于位置 P 的点可以通过坐标找到：

`newP = fabric.util.transformPoint(P, canvas.viewportTransform)；`

`Object.calcTransformMatrix`：返回表示特定时刻通用对象变换的matrix（受`top、left、scale`和许多其他属性的影响），并将点从对象空间移动到canvas空间，但不缩放。因此，在对象空间坐标中给定一个位于坐标 P 处的点，该点将被绘制在canvas上：

`newP = fabric.util.transformPoint(P, object.calcTransformMatrix())；`

### transform顺序
在渲染过程中，Fabric 按以下顺序应用变换：
`zoom and pan => object transformation => nested object ( group ) => additionally nested objects ( nested groups )`

### 恢复顺序
`invertTransform` 工具用于在变换逻辑中后移，以进行一些反向计算：
试想一下，如果您想在canvas上标记一个对象，可以用鼠标单击该对象所在的点。您单击的点是 P，例如该元素上的 10,10 像素。对象会被缩放和旋转，canvas也会被缩放和平移。
要反转渲染计算，可以按照以下逻辑进行：

```javascript
// 计算应用于对象像素的总变换：
var mCanvas = canvas.viewportTransform;
var mObject = object.calcTransformMatrix();
var mTotal = fabric.util.multiplyTransformMatrices(mCanvas, mObject); // 颠倒顺序会导致错误结果
var mInverse = fabric.util.invertTransform(mTotal);
var pointInObjectPixels = fabric.util.transformPoint(pointClicked, mInverse);
```
现在，`pointInObjectPixels` 是坐标空间中的一个点，0，0 处是对象的中心点。
### 了解矩阵的效果
给定`top、left、angle、scaleX、scaleY、skewX、skewY、flipX、flipY`，创建一个表示该变换的矩阵相对简单。
但如何返回矩阵却不是当务之急。矩阵有 6 个维度，由 6 个数字组成，而属性则有 7 个维度，因为我们可以将翻转同化为缩放。矩阵的数量确实是无限的，但可能的属性组合数量却比矩阵的数量大了无限倍。
这就需要使用 `fabric.util.qrDecompose(matrix)`;，它可以为我们解码矩阵。如果给函数一个通用可逆矩阵，它会返回一个包含这些信息的选项对象：
```javascript
{
  angle: number, 
  scaleX: number,
  scaleY: number,
  skewX: number, 
  skewY: 0, //始终是0
  translateX: number,
  translateY: number,
}
```
函数会给出该矩阵的一个可能解，并将偏斜 Y 设为 0。
### 真实用例
一位开发人员希望将对象组合在一起，但同时又要保持它们的自由度。理想情况下，当一个主要对象移动时，他希望其他一些对象也跟着移动。
为了解释这个例子，我将主对象称为 BOSS，其他对象称为 MINIONS。
让我们想象一下，在canvas周围有一些物体，我们可以自由移动它们。在某一时刻，我们希望锁定它们的相对位置，同时缩放并移动其中一个。当我们设置想要的位置时，BOSS 的位置是由一个矩阵来描述的，正如我们现在所学到的，每个 MINION 也是如此。
我确信存在一个矩阵，它定义了从BOSS移动到MINION所需的变换，而我们要找到它。
```html
<canvas id="c" width="600" height="600" style="border: 1px solid #ccc;"></canvas>
<script src="https://cdn.bootcdn.net/ajax/libs/fabric.js/521/fabric.js"></script>
<script>
    const fCanvas = new fabric.Canvas('c')
    const lineArr = []
    for (let i = 0; i < 100; i++) {
        const line = new fabric.Line([i * 10,0,i * 10,1000,], {stroke: 'black',selectable: false,strokeWidth: .3})
        lineArr.push(line)
    }
    for (let i = 0; i < 100; i++) {
    const line = new fabric.Line([0,i * 10,1000,i * 10,], {stroke: 'black',selectable: false,strokeWidth: .3})
        lineArr.push(line)
    }
    const backGroup = new fabric.Group(lineArr, { selectable: false });
    fCanvas.add(backGroup)
    const minion1 = new fabric.Rect({left: 200,top: 100,width: 100,height: 100,fill: 'red',stroke: 'black',strokeWidth: 2,label: 'minion'
    })
    fCanvas.add(minion1)
    const minion2 = new fabric.Rect({left: 100,top: 400,width: 100,height: 100,fill: 'red',stroke: 'black',strokeWidth: 2,label: 'minion'
    })
    fCanvas.add(minion2)
    const boss = new fabric.Circle({radius: 200, fill: 'green', left: 200, top: 200})
    fCanvas.add(boss)
    boss.on('moving', updateMinions);
    boss.on('rotating', updateMinions);
    boss.on('scaling', updateMinions);
    function updateMinions() {
        var minions = fCanvas.getObjects().filter(o => o.label == 'minion');
        minions.forEach(o => {
            if (!o.relationship) {
                return;
            }
            var relationship = o.relationship;
             /*
            使用 fabric.util.multiplyTransformMatrices 函数计算新的变换矩阵 newTransform,该矩阵是bos的变换矩阵(通过 boss.calcTransformMatrix() )与关系矩阵的乘积。
            */
            var newTransform = fabric.util.
                multiplyTransformMatrices(
                boss.calcTransformMatrix(),
                relationship
            );
            /*
            使用 fabric.util.qrDecompose 函数对新的变换矩阵进行 QR 分解，将结果存储在变量 opt 中。
            */
            opt = fabric.util.qrDecompose(newTransform);
            o.set({
                flipX: false,
                flipY: false,
            });
            /*
            使用 setPositionByOrigin 方法根据 opt 中的平移值(translateX 和 translateY)和原点('center')来设置对象 o 的位置。
            */
            o.setPositionByOrigin(
                { x: opt.translateX, y: opt.translateY },
                'center',
                'center'
            );
            /*
            将对象 o 的变换矩阵设置为 opt。调用 o.setCoords() 方法更新对象 o 的坐标。
            */
            o.set(opt);
            o.setCoords();
        });
    }
    fCanvas.on('mouse:down', function (opt) {
        var evt = opt.e;
        var minions = fCanvas.getObjects().filter(o => o.label == 'minion');
        //计算一个boss的变换矩阵并求其逆矩阵。
        var bossTransform = boss.calcTransformMatrix();
        var invertedBossTransform = fabric.util.invertTransform(bossTransform);
        minions.forEach(o => {
            var desiredTransform = fabric.util.multiplyTransformMatrices(
                invertedBossTransform,
                o.calcTransformMatrix()
            );
            if (evt.altKey) {
                o.relationship = desiredTransform;
            } else {
                o.relationship = undefined;
            }
        });
    });
    
</script>
```
//这节没看懂 