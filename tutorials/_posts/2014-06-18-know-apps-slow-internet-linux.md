---
layout: post
date: 2014-06-18
title: كيفية معرفة التطبيقات التي تستهلك سرعة الإنترنت على اللينكس
type: tutorial
---




كثيراً ما يكون هناك تطبيقات غير ظاهرة تعمل في الخلفية وتستهلك سرعة الإنترنت مما يؤدي لبطئ ملحوظ أثناء تصفحنا للإنترنت .. والآن سنتعرف على طريقة من عدة طرق لمعرفة التطبيقات المتصلة بالإنترنت على نظام لينكس ، والطريقة هذه برأيي هي الأفضل حيث أنها تظهر التطبيقات المتصلة والسرعة التي تستهلكها حيث سيظهر التطبيق الذي يستهلك سرعة الإنترنت بشكل كبير أولاً ، وبعد معرفته يمكننا إغلاقه من مدير العمليات system monitor

أولا يجب تنزيل التطبيق nethogs والذي يقوم بذلك من خلال الأمر :


        sudo apt-get install nethogs 


ثم لمشاهدة التطبيقات المتصلة بالإنترنت نكتب :

        sudo nethogs <interface>


مع استبدال `<interface>` بالواجهة التي تتصل من خلالها بالإنترنت ، فإذا كنت تتصل سلكياً بالإنترنت استبدل `<interface>` بـ `eth0` ، واذا كنت تتصل لا سلكياً استبدلها بـ `wlan0` ،(لمشاهدة جميع الواجهات الموجودة في الجهاز اكتب الأمر: `sudo ifconfig` ) .

وبعد مشاهدة التطبيقات اذا كان هناك تطبيق يستهلك سرعة النت وأردت إغلاقة اذهب الى قائمة البرامج وابحث عن
 system monitor ، ستجد تحت تبويب processes أو العمليات جميع التطبيقات المفتوحة وهي مرتبة أبجدياً ، ابحث عن التطبيق الذي تود إغلاقة ثم انقر على End process أو إنهاء العملية .

**ملاحظة:** لإغلاق تطبيق nethogs المفتوح على التيرمينال فقط اضغط 
ctrl + C  ، ثم أغلق التيرمينال