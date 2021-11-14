## 传统布局与流动布局

### 基本布局须知

> 💡首先我们来了解一下盒子模型与行内块元素

#### 盒子模型

1. 概念：

   css定义的所有元素都可以拥有像盒子一样的外形和平面空间，它是css布局的基石

   它规定了网页元素如何显示以及元素间相互关系。  

2. 盒子模型组成：

   - 外边框——margin
   - 边框——border
   - 内边距——padding
   - 内容——content    
   
        ![contentbox.jpg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/118bc90b63714063bb2c42efefca0f6a~tplv-k3u1fbpfcp-watermark.image?)

3. 外边距叠加

   盒模型会发生`margin`外边距叠加，叠加后的值会以最大边距为准。  

   现在我们将两个相邻的`<div>`元素分别设置了大小不同的margin外边距：

   ```html
   <style>
           .box {
               margin: 10px;
               padding: 20px;
               border: solid 2px #000;
           }
           .large-box {
               margin: 20px;
           }
   </style>
   <body>
       <div class="box"></div>
       <div class="large-box box"></div>
   </body>
   ```

    ![边距叠加.jpg](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/76caeaab6125467ea6f69575711b58cf~tplv-k3u1fbpfcp-watermark.image?)

4. 盒子计算

   - content-box

     content-box的计算方程式为：content` + `padding` + `border

   - border-box

     border-box的计算方式为：元素的总宽高为设置的元素宽高
     
        ![content与border.jpg](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/06851c57713b49e0bd0532eb96bb7f67~tplv-k3u1fbpfcp-watermark.image?)

#### 行内元素与块级元素

1. 概念：

   - 行内元素：行内元素是瘦子，可以在一行内一个接一个地挨着
   - 块级元素：块级元素是胖子，一行内只能占一个块级元素  

2. 区别：

   |              行内元素              |           块级元素           |
   | :--------------------------------: | :--------------------------: |
   | 相邻的行内元素会排在同一行，会换行 |       块级元素独占一行       |
   |         宽度随元素内容变化         | 宽度自动填充满其父元素的宽度 |
   |       高度与宽度属性设置无效       |      高度与宽度设置有效      |
   |     外边距与内边距只能设置左右     |  外边距与内边距可以随意设置  |

   行内块元素：结合行内元素与块级元素的特性，即既有block的高宽特性与inline的行内特性

3. 如何设置：

   - 设置为行内元素：

     ```css
     display:inline
     ```

   - 设置为块级元素：

     ```css
     dispaly:block
     ```

   - 设置为行内块元素：

     ```css
     display:inline-block
     ```
     
     ```html
         <style>
          div {
            width: 100px;
            height: 100px;
            text-align: center;
            background-color: brown;
            color: white;
          }
          .inline {
            height: 100px;
            width: 100px;
          }
        </style>
        <div>我是块级元素</div>
        <span class="inline">我是行内元素</span>
        <span class="inline">我也是行内元素</span>
     ```
     
        ![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8a1aedb3226c4528b36752c9d2e9dfa0~tplv-k3u1fbpfcp-watermark.image?)
### 传统布局

#### 文档流

1. 概念：

   文档流即在浏览器中的规则，将窗体自上而下 分成一行一行

   并在每行中按照从左到右依次排放元素，称为文档流。

2. 流动方向：

   - inline元素从左到右，到达最右边才会换行。

   - block元素从上到下，每一个都另起一行。

   - inline-block也是从左到右。

#### 脱离文档流

1. 概念：

   我们不只使用默认文档流来进行我们的布局，那样会很丑

   所以我们可以使我们的元素脱离文档流

2. 如何脱离文档流：

   我们可以通过设置position与float属性来使元素脱离文档流

3. 定位——position

   - 相对定位

     1. 概念：元素以自我为基准进行定位，通过偏移移动至原来的位置上，也就是以自身为参照点

     2. 使用：

        ```css
        position:relative;
        ```

        元素框偏移某个距离，元素仍保持未定位前的形状，它原本所占的空间仍保留

   - 绝对定位

     1. 概念：按照父元素及祖先元素来定位的

     2. 注意：

        - 当他没有父级元素，那么他就根据浏览器来进行偏移

        - 当祖先元素有定位的时候，那么就会以最近一级的有定位上级元素为参考来进行偏移

     3. 使用：

        ```css
        position:absolute;
        ```

   - 固定定位

     1. 概念：以浏览器可视窗口进行定位

     2. 使用：

        ```css
        position:fixed;
        ```
   
4. 定位后的边偏移
   
   - top/bottom
   - left/right
   
5. 通过浮动脱离文档流

   1. 概念：浮动元素会脱离普通流脱离普通流的控制，移动到指定位置

   2. 使用：

      ```css
      float:left;
      float:right;
      ```

   3. 注意：

      - 浮动的盒子不再保留原来的位置，后面的普通流元素会顶上其位置
      - 浮动的元素会一行内显示并且元素顶部对齐
      - 浮动的元素具有行内块的特性

6. 清除浮动

   - 使用：

     ```css
     clear: both;
     ```

   - 为什么要清除浮动？

     因为浮动元素不占用原文档的位置，会对后面的元素排版产生影响

### flex布局

#### 区别与特性

1. 与传统布局对比：

    - 传统布局：基于盒状模型，依赖 display，position，float属性，实现特殊布局很繁琐

    - flex布局：它是一种一维的布局模型，它给 flexbox 的子元素之间提供了强大的空间分布和对齐能力，所以它能很简单地实现一些特殊布局。

2. 特性与概念：

    - 任何一个容器（div）都可以使用flex布局

    - 采用flex布局的元素被成为flex容器，所有子元素都会成为它的成员。

    - 采用flex的元素其float，clear都会失效

    - 一维的特性使其拥有两根轴，水平的主轴与垂直的交叉轴（默认主轴排列）

 

#### 容器属性的使用

1. flex-direction属性  
   flex-direction属性决定主轴的方向

   | 属性值         |            作用            |
   | :------------- | :------------------------: |
   | row            | 主轴为水平方向，起点在左端 |
   | row-reverse    | 主轴为水平方向，起点在右端 |
   | colmun         | 主轴为垂直方向，起点在上端 |
   | colmun-reverse | 主轴为垂直方向，起点在下端 |

2. flex-wrap属性  
   flex属性定义在一条轴线上子成员发生拥挤，如何换行排列。

   | 属性值       |            作用            |
   | :----------- | :------------------------: |
   | nowrap       | 不换行（将子成员宽度缩小） |
   | wrap         |     换行且第一行在上方     |
   | wrap-reverse |     换行且第一行在下方     |

3. justify-content属性  
   justify-content属性定义了项目在主轴上的对齐方式。

   | 属性值        |         作用         |
   | :------------ | :------------------: |
   | flex-start    |        左对齐        |
   | flex-end      |        右对齐        |
   | center        |         居中         |
   | space-between | 两端对齐，且间隔相等 |
   | space-around  |  每个子成员间隔相等  |

4. align-items属性  
   align-items属性定义项目在交叉轴上如何对齐。

   | 属性值     |                        作用                        |
   | :--------- | :------------------------------------------------: |
   | flex-start |                  交叉轴的起点对齐                  |
   | flex-end   |                  交叉轴的终点对齐                  |
   | center     |                  交叉轴的中点对齐                  |
   | baseline   |             项目的第一行文字的基线对齐             |
   | stretch    | 如果项目未设置高度或设为auto，将占满整个容器的高度 |

5. align-content属性  
   align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

   | 属性值     |                             作用                             |
   | :--------- | :----------------------------------------------------------: |
   | flex-start |                      与交叉轴的起点对齐                      |
   | flex-end   |                      与交叉轴的终点对齐                      |
   | center     |                      与交叉轴的中点对齐                      |
   | baseline   | 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍 |
   | stretch    |                      轴线占满整个交叉轴                      |

#### 项目属性的使用

1. order：

   定义项目的排列顺序。数值越小，排列越靠前，默认为0，可以是负数

   ```css
   order:-1;
   ```

2. flex-grow：

   定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大

   如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间  

   ```css
   flex-grow:1;
   ```

3. flex-shrink:

   属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

   如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。

   如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

   ```css
   flex-shrink:0;
   ```

4. flex-basis:

   指定了子项在容器主轴方向上的初始大小，优先级高于自身的宽度width

   ```css
   flex-basis:100%;
   ```

5. align-self

   允许单个项目有与其他项目不一样的对齐方式，可覆盖 `align-items` 属性。

   默认值为 `auto` ，表示继承父元素的 `align-items` 属性

   ```CSS
   align-self:flex-end;
   ```
