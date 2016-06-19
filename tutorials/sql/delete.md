---
layout: post
date: 2016-06-18
title: سلسلة دروس SQL|تصريح DELETE
---

الفهرس :


[الدرس الأول : التعريف بـ SQL](intro)

[الدرس الثاني : بناء SQL](build)

[الدرس الثالث : تصريح SELECT](select)

[الدرس الرابع : تصريح تحديد الاختلاف في SQL](select-distinct)

[الدرس الخامس : عبارة WHERE في SQL](where)

[الدرس السادس : عمليات AND & OR في SQL](and-or)

[الدرس السابع : دالة ORDER BY في SQL](order-by)

[الدرس الثامن: تصريح INSERT INTO في SQL](insert-into)

[الدرس التاسع: تصريح UPDATE في SQL](update)

الدرس العاشر: تصريح DELETE في SQL
*****************



يستخدم تصريح DELETE لحذف تسجيلات من جدول .

* Toc
{:toc}

# بناء DELETE


		DELETE FROM table_name

		WHERE some_column=some_value;


# لاحظ عبارة WHERE في تصريح DELETE !

عبارة WHERE تحدد التسجيل أو التسجيلات التي يجب ان تُحذف ، إذا قمت بحذف عبارة WHERE فسيتم حذف جميع التسجيلات!


# استعراض قاعدة بيانات :



سنستخدم قاعدة البيانات المعروفة جيداً : Northwind


في الأسفل تحديد من جدول الزبائن Customers

![customers](/assets/customers.png)

# مثال على DELETE


على افتراض أننا نريد حذف الزبون "Alfreds Futterkiste" من جدول الزبائن. نستخدم التصريح التالي


		DELETE FROM Customers

		WHERE CustomerName='Alfreds Futterkiste' AND ContactName='Maria Anders';

الآن ، سيبدو جدول الزبائن على الشكل التالي

![customers5](/assets/customers5.png)

# حذف جميع البيانات


من الممكن حذف جميع الصفوف في جدول بدون حذف الجدول . هذا يعني أن تركيب الجدول وخصائصه وفهارسه ستبقى موجودة وسليمة


		DELETE FROM table_name;


    أو


		DELETE * FROM table_name;


> كن حذراً جداً عند حذف تسجيلات، فلا يمكنك التراجع عن هذا الإجراء!

****************


> التالي؟ في الواقع لم أُكمل الترجمة! حيث ترجمت 10 دروس ولم ألحظ إقبالاً عليها.. إذا أعجبتك الدروس ورغبت بتكملتها [فاطلب ترجمة](/about/request) الباقي.