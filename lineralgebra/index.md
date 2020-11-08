# 线性代数笔记

**线性代数笔记记录-1**

<!--more-->

## 1.成绩组成

{{< mermaid >}}
graph TD
	A(最终成绩) -->|80%|B(期末试卷成绩)
	A -->|20%|C(平时成绩)
	C -->D(作业)
	C -->E(考勤)
{{< /mermaid >}}


## 2.二阶行列式
### 2.1组成
$$
二阶行列式，即：D = 
\left|\begin{array}{cccc} 
    a_{11} & a_{12} \\\ 
    a_{21} & a_{22}
\end{array}\right|
=a_{11}a_{22}-a_{12}a_{21}
$$
$$
其中a_{ij}(i=1,2;j=1,2)称为元素\\\ i为行标，表明元素位于第i行；\\\ j为列标，表明元素位于第j列。
$$
### 2.2性质

$$
\left|\begin{array}{cccc} 
    a_{11} & a_{12} \\\ 
    a_{21} & a_{22}
\end{array}\right|
=\left|\begin{array}{cccc} 
    a_{11} & a_{21} \\\ 
    a_{12} & a_{22}
\end{array}\right|
$$

$$
\left|\begin{array}{cccc} 
    ka_{11} & a_{12} \\\ 
    ka_{21} & a_{22}
\end{array}\right|
=\left|\begin{array}{cccc} 
    a_{11} & ka_{21} \\\ 
    a_{12} & ka_{22}
\end{array}\right|
=k\left|\begin{array}{cccc} 
    a_{11} & a_{21} \\\ 
    a_{12} & a_{22}
\end{array}\right|
$$

$$
\left|\begin{array}{cccc} 
    a_{11}+b_{11} & a_{12} \\\ 
    a_{12}+b_{21} & a_{22}
\end{array}\right|
=\left|\begin{array}{cccc} 
    a_{11} & a_{12} \\\ 
    a_{21} & a_{22}
\end{array}\right|
+\left|\begin{array}{cccc} 
    b_{11} & a_{12} \\\ 
    b_{21} & a_{22}
\end{array}\right|
$$

$$
\left|\begin{array}{cccc} 
    a_{11} & a_{12} \\\ 
    a_{21} & a_{22}
\end{array}\right|=-
\left|\begin{array}{cccc} 
    a_{12} & a_{11} \\\ 
    a_{22} & a_{21}
\end{array}\right|,
\left|\begin{array}{cccc} 
    a_{11} & a_{12} \\\ 
    a_{21} & a_{22}
\end{array}\right|=-
\left|\begin{array}{cccc} 
    a_{21} & a_{22} \\\ 
    a_{11} & a_{12}
\end{array}\right|
$$

## 3.三阶行列式

### 3.1组成

$$
\left|\begin{array}{cccc} 
    a_{11} & a_{12} & a_{13} \\\ 
    a_{21} & a_{22} & a_{21} \\\ 
    a_{31} & a_{32} & a_{31} 
\end{array}\right| 称为三阶行列式
$$
### 3.2计算
$$
\left|\begin{array}{cccc} 
    a_{11} & a_{12} & a_{13} \\\ 
    a_{21} & a_{22} & a_{21} \\\ 
    a_{31} & a_{32} & a_{31} 
\end{array}\right| = \\\ 
a_{11}a_{22}a_{33}+a_{12}a_{23}a_{31}+a_{13}a_{21}a_{32}-\\\ a_{13}a_{22}a_{31}-a_{12}a_{21}a_{33}-a_{11}a_{23}a_{32}
$$

![](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200902215533737.png)

![image-20200902215734402](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200902215734402.png)

## 4.n阶行列式

### 4.1定义：

$$
用 n^2 个元素a_{ij} (i, j=1, 2, ..., n)组成的记号
$$

$$
\left|\begin{array}{cccc} 
    a_{11} & a_{12} & ... & a_{13} \\\ 
    a_{21} & a_{22} & ... & a_{13} \\\ 
    ...    & ...    & ... & ...    \\\ 
    a_{31} & a_{32} & ... & a_{13} 
\end{array}\right|元素a_{ij}，i为行标，j为列标
$$


**称为n阶行列式**

### 4.2（代数）余子式

$$
在n 阶行列式中，把元素a_{ij}所在的第i行和第j列划后，\\\ 留下来的n－1阶行列式叫做元素 a_{ij}的余子式，记作M_{ij}.\\\ 把A_{ij}=(-1)^{i+j}M_{ij}称为元素a_{ij}的代数余子式
$$

![image-20200902221152753](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200902221152753.png)

{{< typeit >}}

结论：因为行标和列标可唯一标识行列式的元素，所以行列式中每一个元素都分别对应着一个余子式和一个代数余子式

{{< /typeit >}}

{{< admonition warning "注意" True >}}

注意：当n = 1时，一阶行列式|a| = a，注意不要与绝对值的记号相混淆. 例如：一阶行列式|-1| = -1

{{< /admonition >}}

### 4.3性质

1. 行列式与它的转置行列式相等
2. 互换行列式的两行（列）,行列式变号.
3. 行列式的某一行（列）中所有的元素都乘以同一个倍数  ，等于用数  乘以此行列式.
4. 行列式中如果有两行（列）元素成比例，则此行列式为零．
5. 若行列式的某一列（行）的元素都是两数之和，则行列式可以拆分为两个行列式的和
6. 把行列式的某一列（行）的各元素乘以同一个倍数然后加到另一列(行)对应的元素上去，行列式不变．
