---
title: Git Pull
localeTitle: بوابة سحب
---
## بوابة سحب

`git pull` هو أمر Git يستخدم لتحديث الإصدار المحلي لمستودع من جهاز تحكم عن بعد.

وهو واحد من الأوامر الأربعة التي تحفز التفاعل الشبكي من Git. بشكل افتراضي ، `git pull` يفعل شيئين.

1.  تحديث فرع العمل المحلي الحالي (الفرع المعتمد حاليا)
2.  تحديثات فروع التتبع عن بعد لجميع الفروع الأخرى.

`git pull` جلب الجيت ( `git fetch` ) تلتزم الجديدة [`git merge` ( `git merge` )](https://guide.freecodecamp.org/git/git-merge) هذه في الفرع المحلي.

بناء جملة هذا الأمر هو كما يلي:

 `# General format 
 git pull OPTIONS REPOSITORY REFSPEC 
 
 # Pull from specific branch 
 git pull REMOTE-NAME BRANCH-NAME 
` 

بحيث:

*   **الخيارات** هي خيارات الأوامر ، مثل `--quiet` أو `--verbose` . يمكنك قراءة المزيد عن الخيارات المختلفة في [وثائق Git](https://git-scm.com/docs/git-pull)
*   **REPOSITORY** هو عنوان URL الخاص بك. مثال: https://github.com/freeCodeCamp/freeCodeCamp.git
*   تحدد **REFSPEC** أي من **الحزم** الذي **سيتم جلبه والحلول** المحلية المراد تحديثها
*   **REMOTE-NAME** هو اسم مستودع التخزين عن بعد. على سبيل المثال: _الأصل_ .
*   **BRANCH-NAME** هو اسم الفرع الخاص بك. على سبيل المثال: _تطوير_ .

**ملحوظة**

إذا كان لديك تغييرات غير ملتزم بها ، فسوف تفشل عملية دمج الأمر `git pull` وسيتم إلغاء الفرع المحلي الخاص بك.

وبالتالي ، يجب عليك _دائمًا الالتزام بتعديلاتك في فرع قبل سحب_ طلبات جديدة من مستودع بعيد.

**جدول المحتويات**

*   [باستخدام `git pull`](#using-git-pull)
*   [تحكم الإصدار الموزع](#distributed-version-control)
*   [`git fetch` + `git merge`](#git-fetch-plus-git-merge)
*   [`git pull` في IDEs](#git-pull-in-IDEs)

### باستخدام سحب بوابة

استخدم `git pull` لتحديث مستودع محلي من مستودع بعيد عن بعد. على سبيل المثال: أثناء العمل محليًا على الصفحة `master` ، يمكنك تنفيذ `git pull` لتحديث النسخة المحلية من `master` وتحديث فروع التتبع عن بُعد الأخرى. (مزيد من المعلومات حول فروع التتبع عن بُعد في القسم التالي.)

ولكن هناك بعض الأمور التي يجب تذكرها في هذا المثال:

*   يحتوي المستودع المحلي على مستودع تخزين بعيد مرتبط
*   تحقق هذا عن طريق تنفيذ `git remote -v`
*   إذا كان هناك أجهزة `git pull` عن بعد متعددة ، فقد لا يكون `git pull` معلومات كافية. قد تحتاج إلى إدخال `git pull origin` أو `git pull upstream` .
*   يحتوي الفرع الذي تم سحبه حاليًا على فرع تتبع عن بعد
*   تحقق من هذا عن طريق تنفيذ `git status` . إذا لم يكن هناك فرع تتبع عن بعد ، لا يعرف Git مكان سحب المعلومات _منه_ .

### تحكم الإصدار الموزع

Git هو **نظام التحكم في إصدار الموزعة** (DVCS). مع DVCS ، يمكن للمطورين العمل على نفس الملف في نفس الوقت في بيئات منفصلة. بعد _دفع_ الكود إلى مستودع بعيد مشترك ، يمكن للمطورين الآخرين _سحب_ التعليمات البرمجية التي تم تغييرها.

#### تفاعلات الشبكة في Git

لا يوجد سوى أربعة أوامر تطالب بتفاعلات الشبكة في Git. لا يوجد لدى المستودع المحلي أي وعي بالتغييرات التي تم إجراؤها على المستودع البعيد حتى يكون هناك طلب للحصول على معلومات. والمستودع عن بعد ليس لديه وعي بالتغييرات المحلية حتى يتم دفع الإلتزامات.

أوامر الشبكة الأربعة هي:

*   `git clone`
*   `git fetch`
*   `git pull`
*   `git push`

#### الفروع في DVCS

عند العمل مع Git ، يمكن أن تشعر أن هناك الكثير من نسخ الشفرة نفسها التي تطفو في كل مكان. هناك إصدارات مختلفة من نفس الملف على كل فرع. ونسخ مختلفة من نفس الفروع على كل كمبيوتر المطور وعلى جهاز التحكم عن بعد. لتتبع هذا ، يستخدم Git شيئًا يسمى **فروع التتبع عن بُعد** .

إذا قمت بتنفيذ `git branch --all` داخل مستودع Git ، تظهر فروع التتبع عن بعد باللون الأحمر. هذه هي نسخ للقراءة فقط من التعليمات البرمجية كما تظهر على جهاز التحكم عن بعد. (متى كان آخر تفاعل على الشبكة قد جلب المعلومات محليًا؟ تذكر متى تم تحديث هذه المعلومات آخر مرة. تعكس المعلومات الواردة في فروع التتبع عن بعد المعلومات من هذا التفاعل).

مع **فروع التتبع عن بعد** ، يمكنك العمل في Git على عدة فروع بدون تدخل الشبكة. في كل مرة تنفذ فيها أوامر `git pull` أو `git fetch` ، يمكنك تحديث **فروع التتبع عن بُعد** .

### git fetch plus git merge

`git pull` هو أمر `git fetch` ، يساوي `git fetch` + `git merge` .

#### جلبه

من تلقاء نفسه ، `git fetch` التحديثات جميع فروع التتبع عن بعد في المستودع المحلي. لا تنعكس أي تغييرات في الواقع على أي من فروع العمل المحلية.

#### اندماج

وبدون أي حجج ، سيقوم `git merge` فرع التتبع عن بعد المقابل إلى فرع العمل المحلي.

#### سحب بوابة

`git fetch` تحديثات عن بعد فروع الفروع. `git merge` بتحديث الفرع الحالي بفرع التتبع البعيد المطابق. باستخدام `git pull` ، ستحصل على كلا جزئي هذه التحديثات. ولكن ، هذا يعني أنه إذا تم سحبك `feature` الفرع وقمت بتنفيذ `git pull` ، عند إجراء السحب `master` ، لن يتم تضمين أية تحديثات جديدة. عندما تقوم بالسداد إلى فرع آخر قد يكون لديه تغييرات جديدة ، فمن الأفضل دائمًا تنفيذ `git pull` .

### سحب بوابة في IDEs

قد لا تتضمن اللغة الشائعة في IDES الأخرى الكلمة `pull` . إذا نظرت إلى كلمات `git pull` ولكن لا تراها ، فابحث عن كلمة `sync` بدلاً من ذلك.

### fethcing PR البعيد (سحب الطلب) في الريبو المحلي

ولأغراض المراجعة ، يجب جلب المستفيدين الرئيسيين في المناطق النائية إلى الريبو المحلي. يمكنك استخدام أمر `git fetch` النحو التالي لتحقيق ذلك.

`git fetch origin pull/ID/head:BRANCHNAME`

المعرف هو معرف طلب السحب و BRANCHNAME هو اسم الفرع الذي تريد إنشاءه. بمجرد إنشاء الفرع ، يمكنك استخدام `git checkout` للتبديل إلى هذه الفرشاة.

### موارد أخرى على سحب جيت

*   [GIT-المجلس الأعلى للقضاء](https://git-scm.com/docs/git-pull)
*   [جيثب مساعدة مستندات](https://help.github.com/articles/fetching-a-remote/#pull)
*   [جيثب عند الطلب التدريب](https://services.github.com/on-demand/intro-to-github/create-pull-request)
*   [مزامنة البرامج التعليمية](https://www.atlassian.com/git/tutorials/syncing)

### موارد أخرى على بوابة في guide.freecodecamp.org

*   [اندماج Git](../git-merge/index.md)
*   [بوابة الخروج](../git-checkout/index.md)
*   [ارتكاب بوابة](../git-commit/index.md)
*   [خبأ جيت](../git-stash/index.md)
*   [فرع جيت](../git-branch/index.md)