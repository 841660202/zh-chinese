.. index:: ! operator

运算符
=========

即使两个操作数的类型不一样，也可以应用算术和位操作数。
例如，您可以计算 ``y = x + z``，其中 ``x`` 是 ``uint8``， ``z`` 的类型为 ``int32``。
在这种情况下，下面的机制将被用来确定计算操作的类型（这在溢出的情况下很重要）和操作结果的类型：

1. 如果右操作数的类型可以隐式转换为左操作数的类型，则使用左操作数的类型，
2. 如果左操作数的类型可以隐式转换为右操作数的类型，则使用右操作数的类型，
3. 否则的话，该操作不被允许。

<<<<<<< HEAD
如果其中一个操作数是 :ref:`字面常数 <rational_literals>`，
它首先被转换为其 “移动类型（mobile type）”，也就是能容纳该值的最小类型
（相同位宽的无符号类型被认为比有符号类型 "小"）。
如果两者都是字面常数，则以任意的精度进行计算。
=======
In case one of the operands is a :ref:`literal number <rational_literals>` it is first converted to its
"mobile type", which is the smallest type that can hold the value
(unsigned types of the same bit-width are considered "smaller" than the signed types).
If both are literal numbers, the operation is computed with effectively unlimited precision in
that the expression is evaluated to whatever precision is necessary so that none is lost
when the result is used with a non-literal type.
>>>>>>> 8df45f5f8632da4817bc7ceb81497518f298d290

操作符的结果类型与操作的类型相同，除了比较操作符，其结果总是 ``bool``。

运算符 ``**`` （幂运算）， ``<<`` 和 ``>>`` 使用左边操作数的类型进行运算和以其作为结果。

三元运算符
----------------
三元运算符用于形式为 ``<条件表达式> ? <true条件表达式> : <false条件表达式>``。
它根据主要的 ``<条件表达式>`` 的评估结果，计算后两个给定表达式中的一个。
如果 ``<条件表达式>`` 评估为 ``true``，那么 ``<true条件表达式>`` 将被计算，否则 ``<false条件表达式>`` 被被计算。

三元运算符的结果没有有理数类型，即使它的操作数都是有理数字。
结果类型是由两个操作数的类型决定的，方法同上，如果需要的话，首先转换为它们的可移动计算的类型。

因此， ``255 + (true ? 1 : 0)`` 将由于算术溢出而恢复计算。
原因是 ``(true ? 1 : 0)`` 是 ``uint8`` 类型，这迫使加法也在 ``uint8`` 中进行，
而256超出了这个类型允许的范围。

另一个结果是，像 ``1.5 + 1.5`` 这样的表达式是有效的，但 ``1.5 + (true ? 1.5 : 2.5)`` 却无效。
这是因为前者是一个以无限精度计算的有理表达式，只有它的最终值才是重要的。
后者涉及到将小数有理数转换为整数，这在目前是不允许的。

.. index:: assignment, lvalue, ! compound operators

复数和增量/减量运算符
----------------------

如果 ``a`` 是一个LValue（即是一个变量或者是可以被分配的东西），
下列运算符可以作为速记：

``a += e`` 相当于 ``a = a + e``，运算符 ``-=``， ``*=``， ``/=``， ``%=``，
``|=``， ``&=``， ``^=``， ``<<=`` 和 ``>>=`` 都有相应的定义。
``a++`` 和 ``a--`` 相当于 ``a += 1`` / ``a -= 1`` 但是表达式本身仍然是以前的值 ``a``。
相比之下， ``--a`` 和 ``++a`` 对 ``a`` 有同样的作用，但返回改变后的值。

.. index:: !delete

.. _delete:

删除
------

``delete a`` 为该类型分配初始值 ``a``。例如，对于整数来说，它相当于 ``a = 0``，
但是它也可以用于数组，它指定一个长度为0的动态数组或者一个相同长度的静态数组，
所有元素都设置为初始值。 ``delete a[x]`` 删除数组中索引为 ``x`` 的元素，
并保留所有其他元素和数组的长度不动。这特别意味着它在数组中留下一个缺口。
如果您打算删除项目，一个 :ref:`映射类型 <mapping-types>` 可能是一个更好的选择。

对于结构体，则将结构体中的所有属性重置。换句话说，在 ``delete a`` 之后，
``a`` 的值与 ``a`` 在没有赋值的情况下被声明是一样的，但有以下注意事项：

``delete`` 对映射类型没有影响（因为映射的键可能是任意的，通常是未知的）。
因此，如果您删除一个结构体，它将重置所有不是映射类型的成员，
同时也会递归到这些成员，除非它们是映射。
然而，单个键和它们所映射的内容可以被删除。
如果 ``a`` 是一个映射，那么 ``delete a[x]`` 将删除存储在 ``x`` 的值。

值得注意的是， ``delete a`` 的行为实际上是对 ``a`` 的赋值，
也就是说，它在 ``a`` 中存储了一个新的对象。
当 ``a`` 是引用变量时，这种区别是明显的。
它只会重置 ``a`` 本身，而不是它之前引用的值。

.. code-block:: solidity

    // SPDX-License-Identifier: GPL-3.0
    pragma solidity >=0.4.0 <0.9.0;

    contract DeleteExample {
        uint data;
        uint[] dataArray;

        function f() public {
            uint x = data;
            delete x; // 将 x 设为 0，并不影响data变量
            delete data; // 将 data 设为 0，并不影响 x
            uint[] storage y = dataArray;
            delete dataArray; // 将 dataArray.length 设为 0，但由于 uint[] 是一个复杂的对象，
            // y 也将受到影响，它是一个存储位置是 storage 的对象的别名。
            // 另一方面："delete y" 是非法的，引用了 storage 对象的局部变量只能由已有的 storage 对象赋值。
            assert(y.length == 0);
        }
    }

.. index:: ! operator; precedence
.. _order:

运算符的优先顺序
--------------------------------

.. include:: types/operator-precedence-table.rst
