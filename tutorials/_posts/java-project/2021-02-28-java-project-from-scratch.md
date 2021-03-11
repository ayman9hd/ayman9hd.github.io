---
layout: post
date: 2021-02-28
title: بناء تطبيق جافا إف إكس من الصفر
description: شرح عمل تطبيق بلغة جافا مع واجهة JavaFX وقاعدة بيانات MySQL من الصفر
type: tutorial
tags: [برمجة, تعليم, Java]
---


مرحبًا.. سأشرح في هذا المقال كيفية عمل تطبيق جافا للحاسوب مع واجهة (JavaFX) وقاعدة بيانات (MySQL)، أي بناء تطبيق متكامل ومن الصفر. النتيجة النهائية لهذا التطبيق ستكون على الشكل التالي:

نافذة تسجيل الدخول

  {% include image.html layout="responsive" width="400" height="250" src="https://raw.githubusercontent.com/Mulham/Java-Project/images/images/UI1.png" alt="بناء تطبيق جافا FX من الصفر -1" %}


النافذة الرئيسية
{% include image.html layout="responsive" width="400" height="250" src="https://raw.githubusercontent.com/Mulham/Java-Project/images/images/UI2.png" alt="بناء تطبيق جافا FX من الصفر -2" %}

نافذة تحرير المستخدمين حيث يمكن إضافة وحذف مستخدم أو تعديل بياناته

  {% include image.html layout="responsive" width="400" height="250" src="https://raw.githubusercontent.com/Mulham/Java-Project/images/images/UI3.png" alt="بناء تطبيق جافا FX من الصفر -3" %}

وما إلى ذلك..

سأضع لك عند بعض المراحل في الشرح رابطًا للكود البرمجي في حالته عند تلك المرحلة.
والكود النهائي للتطبيق تجده [هنا](https://github.com/Mulham/Java-Project) 

* Toc
{:toc}

# ماهي JavaFX

باختصار هي عبارة عن منصة **لعمل واجهة** لتطبيقات الجافا، أي لا يمكن عمل تطبيق جافا **مع واجهة** بدونها (أو بدون أحد بديلاتها)،  منصة Swing موجودة ومستخدمة لعمل الواجهات مع الجافا قبل وجود جافا إف إكس، وقد وُضِعت الأخيرة لاستبدال Swing، وتعتبر أفضل من swing في كثير من الأمور منها ماهو برمجي أيضًا حيث تفصل جافا إف إكس ملفات الواجهة عن ملفات الجافا وبالتالي يكون الكود أكثر تنسيقا مما هو عليه في swing.

يمكن مع جافا إف إكس عمل تطبيقات للحاسوب وللموبايل وكذلك للوب.


# البرامج والمكتبات المستخدمة

فيما يلي البرامج والأدوات اللازمة والتي يجب تنصيبها لتنفيذ التطبيق:

قم بتنصيب البرامج التالية: 

* بالنسبة لمحرر الكود (IDE) فسيتم الشرح باستخدام [IntelliJ Edu](https://www.jetbrains.com/idea/download) وهو مجاني


* محرر الواجهة [Gluon scene builder](https://gluonhq.com/products/scene-builder/#download) حيث أن مزايا محرر الواجهة الافتراضي والذي يأتي مع محرر الكود محدودة نوعا ما

* [MySQL Server](https://dev.mysql.com/downloads/mysql/) من أجل قواعد البيانات. ولشرح تنصيبه على اللينكس اضغط [هنا](https://mulham.github.io/mysql-ubuntu/).

* تطبيق [MySQL workbench](https://www.mysql.com/products/workbench/) لعمل مخطط لقاعدة البيانات وتحويله لقاعدة بيانات SQL


ثم قم بتنزيل الملفات التالية وفك الضغط عنها لأشرح لك لاحقًا كيفية إضافتها لتطبيقك:

* [JavaFX SDK](https://gluonhq.com/products/javafx/)
 
* مكتبة [Mysql connector](https://dev.mysql.com/downloads/connector/j/) للربط بقاعدة البيانات. (اختر من القائمة Platform Independent وقم بتحميل الملف المضغوط ثم فك الضغط عنه).


[comment]: # والمكتبات التالية يمكنك تنزيلها ولكنها خاصة بتطبيقنا هنا وتتيح إمكانية تصدير التقارير المنشأة عبر تطبيقنا إلى ملفات إكسل و PDF:

[comment]: # * مكتبة [Poi](https://poi.apache.org/download.html) (Binary Distribution) 

[comment]: # * مكتبة [xmlbeans](https://xmlbeans.apache.org/download/index.html) (Binary Distribution)

[comment]: # * [aspose cells](https://repository.aspose.com/webapp/#/artifacts/browse/tree/General/repo/com/aspose/aspose-cells/21.2/aspose-cells-21.2.jar)

{: .notice}
**ملاحظة:** الكثير من الشروحات تتحدث عن إضافة مكتبة Jfoenix لتحسين جمالية التطبيق، إلا أن تلك المكتبة قد توقف دعمها ولم تعد تعمل مع الإصدارات الحديثة من بيئة عمل جافا FX (بعد الإصدار 11 من JavaFX SDK)


{: .notice}
**ملاحظة2:** وفقًا لما ذُكر فليس من المستحسن إطلاقًا الاعتماد دائمًا على مكتبات خارجية في تطبيقك، ﻷن تلك المكتبات قد يتوقف دعمها (لا يستمر تحديثها) وبالتالي يصبح تطبيقك بالكامل غير صالح عند نقظة زمنية محددة وسيحتاج للتعديل بالكامل ليعمل من جديد. وإن أردت استخدام مكتبة خارجية فتأكد من أنها شائعة وأن مستخدموها كثر وأنها تُحدَّث بشكل دوري.


# وصف المشروع

لدينا مؤسسة تقوم بفحص الأجهزة الطبية وإعطاء تقرير عنها، المطلوب في هذا المشروع هو أتمتة التقرير حول الأجهزة الطبية، حيث كانت تلك المؤسسة تعمل على برنامج الإكسل وفق الجداول لإنتاج وطباعة التقارير المتعلقة بالأجهزة الطبية وتريد تحويل هذه العملية لتطبيق بحيث يقوم هذا التطبيق بترشيح القيم المراد إدخالها تلقائيًا وبعدم قبول القيم غير الصحيحة (والمعرفة مسبقًا) وبالتالي تقليل الأخطاء أثناء ملء وإنتاج تلك التقارير وتسهيل العملية أيضًا.

لذا فإن هذا التطبيق الذي سنقوم ببناؤه سوية يحوي نافذة تسجيل دخول ثم النافذة الرئيسية التي تحوي عدة أقسام (أزرار تأخذ لنافذات مستقلة) بحيث يمكن للمستخدم إضافة مستخدمين وتعديل بياناتهم وحذفهم، وكذلك إضافة شركات بنفس الطريقة والخيارات، كما يمكن إضافة عناصر لقاعدة البيانات وهي الأجهزة الطبية المستخدمة وتاريخ صيانتها الدوري، بالإضافة للمعلومات الخاصة بالتقارير الطبية ذاتها.

التقرير الطبي المراد أتمتته يمكن الوصول له من [هنا](https://github.com/Mulham/Java-Project/blob/main/report.pdf) حيث ستلاحظ وجود عدة أقسام في التقرير، القسم الأول معلومات عامة عنه وعن الزبون (الشركة المتقدمة لفحص الجهاز الطبي) والقسم الثاني معلومات عن الجهاز ثم القسم الثالث نتائج التقرير والفحص وأخيرا معلومات الأشخاص الذين قاموا بإنتاج هذا التقرير.

والآن لنقم بالبدء بالمشروع..

لعمل تطبيق مثل هذا يجب أولًا اعتماد هيكلية التطبيق، وكأي عمارة نريد بناؤها لابد من موجود مخطط من قبل المهندس المعماري قبل البدء بالبناء، هنا أيضًا لابد لمهندس البرمجيات من أن يضع المخطط والهيكلية التفصيلية للتطبيق قبل الشروع بالتنفيذ والبرمجة.


{: .notice}
**ملاحظة:** من المهم جدا عند التعامل مع العميل معرفة كل مايدور برأسه قبل الشروع في العمل. مثلا من غير الكافي أن يتكلم العميل عن وصف المشروع أعلاه لكي تبدأ بالعمل! لا بد من أن تطرح عليه الكثير من الأسئلة عن وظائف التطبيق وآلية عمله ومظهره وعدد نوافذه وحجمها ولونها وكل شيئ قبل البدء.


# تخطيط قاعدة البيانات

سنقوم بهذا المشروع باستخدام قاعدة بيانات MySQL، إن لم يكن لديك معرفة بلغة قواعد البيانات SQL فيمكنك الاطلاع على [سلسلة دروس SQL](https://mulham.github.io/sql/intro)

وفق الأقسام التي رأيناها في التقرير أعلاه يمكن تقسيم قاعدة البيانات إلى الجداول التالية:

* جدول المستخدمين
* جدول الشركات (الزبائن)
* جدول الأجهزة
* جدول التقرير والذي يضم معلومات التقرير عموما
* جدول نتائج التقرير

بالإضافة لجداول أخرى مرتبطة بهذه الجداول وفقا لما هو مطلوب في التقرير، مخطط قاعدة البيانات لدينا هو على الشكل التالي:

  {% include image.html layout="responsive" width="400" height="500" src="https://raw.githubusercontent.com/Mulham/Java-Project/images/images/databas_schema.png" alt="مخطط قاعدة بيانات SQL قابل للتنفيذ" %}


يمكنك مشاهدة الملف الأصلي لمخطط قاعدة البيانات من [هنا](https://github.com/Mulham/Java-Project/blob/main/database_schema.mwb) وهو قابل للتشغيل والتنفيذ على برنامج MySQL Workbench، حيث تم رسم المخطط وعمله على ذلك البرنامج والذي يمكّن من تحويل هذا المخطط لاحقا إلى قاعدة بيانات SQL وفق الخطوات التالية:

قم بفتح ملف "database_schema.mwb" عبر برنامج MySQL Workbench ثم اضغط في الأعلى على الخيار "Database" ثم اختر "Forward Engineer" كما في الصورة:

{% include image.html layout="responsive" width="400" height="300" src="https://raw.githubusercontent.com/Mulham/Java-Project/images/images/mysql-workbench-forward-engineering.png" alt="تحويل مخطط قاعدة البيانات إلى كود SQL" %}


بعدها يمكنك قبول الإعدادات الافتراضية والضغط بشكل متتابع على زر Next إلى أن يتم إعطاء كود SQL الخاص بالمخطط ثم قم بإنهاء العملية ليتم تلقائيًا إنشاء قاعدة البيانات لديك وفق المخطط وكود SQL المُنشأ تلقائيًا. ستجد قاعدة البيانات "mydb" على القائمة اليسارية كما في الصورة:

{% include image.html layout="responsive" width="400" height="300" src="https://raw.githubusercontent.com/Mulham/Java-Project/images/images/mysql-workbench-databases.png" alt="بناء تطبيق جافا FX مع قاعدة بيانات من الصفر" %}





# تخطيط البرنامج

المخطط العام للبرنامج سيكون على النحو التالي:

{% include image.html layout="responsive" width="400" height="300" src="https://raw.githubusercontent.com/Mulham/Java-Project/images/images/software_architecture.png" alt="مخطط وهيكلية برنامج جافا" %}

حيث سنستخدم للواجهة والتي يطلق عليها Frontend عادة: JavaFX وسيُقسم البرنامج إلى أربعة أقسام أو مجلدات: models وهي الكيانات المستخدمة في التطبيق مثل المستخدمين والشركات، و controllers أصناف الجافا التي تربط الواجهة بالدالات والوظائف المناسبة (أي تتحكم بالواجهة)، animations هذه للجماليات لإضافة حركة لبعض الحقول في الواجهة، وطبعا المكتبات المستخدمة في التطبيق libraries (تم إزالة هذا القسم للأسباب المذكورة أعلاه)

أيضًا لا بد من عمل مخطط لعرض أصناف الجافا التي سيتم كتابتها وبكل تفصيلها قبل البدء بالتنفيذ، وهذا يدعى مخطط الصنف في UML يمكنك الاطلاع على طريقة عمله من [هنا](https://mulham.github.io/uml-class-diagram/) ، ومخطط الصنف في حالتنا هذه سيكون على الشكل التالي


{% include image.html layout="responsive" width="400" height="500" src="https://raw.githubusercontent.com/Mulham/Java-Project/images/images/uml-class-diagram.png" alt="مخطط الصنف لتطبيق جافا" %}


# تقرير وصف المشروع

كما ذكرت فيجب قبل البدء بالمشروع وضع مخططات للمشروع ووصفها بكامل تفاصيلها لتصف المشروع بدقة ليكون قابل للتنفيذ وفق التقرير المُعطى من قبل مهندس البرمجيات، هذا التقرير يحوي عادة شرح عام للمشروع وللمشكلة التي يعالجها وكيف سيقوم بحل تلك المشكلة وآلية عمل المشروع والوظائف التي سيحتويها ويقدمها وحالات استخدامه بالإضافة لمخطط قاعدة البيانات ومخطط الصنف المذكورين أعلاه وغيرها من المخططات اللازمة، يكون هذا التقرير عادة عبارة عن 30 صفحة فأكثر بحسب حجم البرنامج.

# التنفيذ

نأتي الآن بعد وضع المخططات وكتابة التقرير وتهيئة قاعدة البيانات إلى الجزء التنفيذي وهو البرمجة بلغة جافا وعمل الواجهة باستخدام JavaFX. وقد قسمت هذا القسم إلى عدة دروس وفقًا للمهام المنجزة فيها: 


1. [تهيئة بيئة العمل](/javafx-initialization)

2. [هيكلة المشروع](/java-project-structure)

3. [تصميم الواجهة](/javafx-interface-design)

4. [الربط مع قاعدة البيانات](/java-database-handler)

5. [تسجيل الدخول](/java-sign-in)

6. [الانتقال بين النوافذ](/javafx-scene-changer)

7. [إدارة المستخدمين](/javafx-manage-users)

8. [إرسال بيانات من نافذة ﻷخرى](/javafx-transfer-data-between-scenes)

9. [النهاية](/javafx-working-process)



**المراجع**

* <https://www.youtube.com/playlist?list=PLHdQfj3Nty4VulBDyryc5M9zfXwWo49Mc>
