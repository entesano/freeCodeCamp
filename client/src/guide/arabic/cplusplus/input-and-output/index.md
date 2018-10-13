---
title: Input and Output
localeTitle: المدخلات والمخرجات
---
## المدخلات والمخرجات مع تيارات

لطباعة الأشياء إلى وحدة التحكم ، أو القراءة منها ، يمكنك استخدام `cout` و `cin` ، اللذان يطلق عليهما `streams` . يتم استخدام هذه الاستعارة نظرًا لأنك تستخدم تدفقات مثل استخدامك لحوض أو نقرة: إما أن تقوم بإسقاط البيانات إلى حوض ( `cout` ) أو الحصول على بيانات من صنبور ( `cin` ).

### الإخراج مع cout

يستخدم برنامج "Hello World" `cout` لطباعة "Hello World!" إلى وحدة التحكم:

 `#include<iostream> 
 using namespace std; 
 
 int main() 
 { 
  cout << "Hello world!" << endl; 
 } 
` 

أول سطرين في الأعلى ضروريان لاستخدام `cout` ومجموعات التدفقات الأخرى. `#include<iostream>` يجعل كائنات الدفق متاحة ، `using namespace std;` يتيح لك كتابة `cout` مباشرة بدلاً من الاضطرار إلى كتابة `std::cout` ، وهذا يعني أن نحتاج إلى استخدام `cout` من مساحة الاسم `std` .

`cout` لتقف على "وحدة التحكم الإخراج" ، وهو ما يسمى _تيار الإخراج_ الذي يمثل وحدة التحكم. عندما تريد طباعة شيء إلى وحدة التحكم ، يمكنك وضعه في `cout` ؛ تخيل أنها حفرة تؤدي إلى المحطة. لوضع الأشياء في هذه الحفرة ، في وقت واحد ، يمكنك استخدام `<<` المشغل ، ويعرف أيضا باسم _مشغل الإدراج_ 1 . يمكن تقييد المشغل ، أي يمكنك وضع عدة أشياء في واحد تلو الآخر. سوف يطبع التالي "الكعكة هي كذبة.":

`cout << "The cake " << "is " << "a " << "lie." << endl;`

`endl` لتقف على "End Line" وهو عنصر آخر يأتي من `<iostream>` . عند وضع `endl` في `cout` ، ستقوم بطباعة حرف السطر الجديد ("\\ n") إلى وحدة التحكم ، وكذلك _مسح_ `cout` ، مما يعني أنه سيجبر `cout` على طباعة كل شيء قمت بوضعه فيه _الآن_ . إذا كنت لا تضع `endl` إلى `cout` ، `cout` قد حفاظ على البيانات التي قد وضعت في ذلك، ولكن تنتظر المزيد من البيانات قبل طباعة كل ذلك في الواقع. هذا يسمى _التخزين المؤقت_ وهو جيد جدًا للأداء ، ولكن إذا كنت قد قدمت بالفعل كل شيء من المفترض طباعته ، فأنت تريد أن `cout` على الفور. لذلك من الممارسات الجيدة أن تنتهي مع `endl` في الأماكن التي يكون لها معنى.

يمكن وضع كل شيء تقريبًا في جدول: السلاسل ، والأرقام ، والمتغيرات ، والتعبيرات ، وما إلى ذلك. في ما يلي بعض الأمثلة على عمليات إدراج البث الصحيحة:

 ``// Notice we can use the number 42 and not the string "42". 
 cout << "The meaning of life is " << 42 << endl;` // Output: The meaning of life is 42 
`` 

 ``string name = "Tim"; 
 cout << "Except for you, " << name << endl;`// Output: Except for you, Tim 
`` 

 ``string name = "Tim"; 
 cout << name; 
 cout << " is a great guy!" << endl;` 
 // Output: Tim is a great guy! 
`` 

 ``int a = 3; 
 cout << a*2 + 18/a << endl;`// Output: 12 
`` 

### ملاحظة حول المسافة البيضاء

C ++ دائما يضع _لكم_ في السيطرة، ويفعل بالضبط فقط الأشياء التي تقول أن تفعله. قد يكون هذا مفاجئًا في بعض الأحيان ، كما في المثال التالي:

 `string name = "Sarah"; 
 cout << "Good morning" << name << "how are you today? << endl; 
` 

قد تتوقع أن تطبع "صباح الخير يا سارة كيف حالك اليوم؟" ، ولكن في الواقع ، سيكون الناتج "Good morningSarahhow هل أنت اليوم؟". سبب هذا الخطأ هو أنك لم تكتب مسافات في السلاسل المحيطة `name` ، وحيث أنك لم تحدد أي مسافات ، فإن `cout` لم يقم بطباعة أي منها. النسخة الصحيحة ستكون: `cout << "Good morning " << name << " how are you today? << endl;`

لا تحدث فواصل الأسطر من تلقاء نفسها. قد تعتقد أن هذا من شأنه أن يطبع وصفة على أربعة أسطر:

 `cout << "To make bread, you need:"; 
 cout << "* One egg"; 
 cout << "* One water"; 
 cout << "* Two wheat"; 
` 

لكن المخرج هو في الواقع على سطر واحد: "لصنع الخبز ، تحتاج: \* بيضة واحدة \* ماء واحد \* اثنين من القمح". هذا لأنه لا توجد أحرف سطر جديد في نهاية الأسطر ، لذا بشكل طبيعي ، تفترض C ++ أننا لا نريدها أن تطبع أحرف السطر الجديد.

يمكنك إصلاح هذا عن طريق إضافة `endl` s بعد كل سطر ، لأنه كما تمت مناقشته سابقًا ، يدرج `endl` حرفًا في السطر الجديد في دفق الإخراج. ومع ذلك ، فإنه يفرض أيضًا أن يتم مسح المخزن المؤقت ، الأمر الذي يفقدنا بعض الأداء لأننا قد قمنا بطباعة جميع الخطوط دفعة واحدة. لذلك سيكون الأفضل إضافة أحرف سطر جديد فعليًا في نهاية الأسطر ، واستخدام `endl` فقط في النهاية:

 `cout << "To make bread, you need:\n"; 
 cout << "* One egg\n"; 
 cout << "* One water\n"; 
 cout << "* Two wheat" << endl; 
` 

إذا كنت تقوم فقط بطباعة وصفة صغيرة ، فإن الوقت الذي تقوم فيه بالحفظ يكون ضئيلًا ولا يستحق العناء ، ولكن إذا كنت تطبع ملايين العناصر ، فقد يكون الفرق ملحوظًا جدًا.

### المدخلات مع السينما

لقراءة من وحدة التحكم، يمكنك استخدام _دفق الإدخال_ `cin` بالطريقة نفسها كما تفعل `cout` ، ولكن بدلا من وضع الأمور في `cin` ، وانت "إخراجهم". يقرأ البرنامج التالي رقمين من المستخدم ويضيفهما معًا:

 `#include<iostream> 
 using namespace std; 
 
 int main() 
 { 
  int a, b; // Variables to hold the two numbers. 
 
  cout << "Please enter the first number:" << endl; 
  cin >> a; 
  cout << "Please enter the second number:" << endl; 
  cin >> b; 
 
  cout << "The sum of your numbers is: " << a + b << endl; 
 } 
` 

يقف `cin` لـ "Console Input" وهو _دفق_ إدخال يمثل الإدخال من وحدة التحكم. في التعبير `cin >> a;` يتم قراءة البيانات من `cin` وحفظها في المتغير `a` ، باستخدام المشغل `>>` ، _عامل الاستخراج_ 2 . يقرأ عامل الاستخراج بالضبط نفس القدر المطلوب من البيانات للكتابة في المتغير الذي نحدده ، ويتخطى أي مسافة بيضاء ، لذلك إذا كان المستخدم يكتب "6" التي ستقرأ فقط كقيمة `6` .

تجدر الإشارة إلى أن `cin` ستوقف البرنامج بأكمله لانتظار أن يكتب المستخدم قيمه. لن يستمر البرنامج حتى يقوم المستخدم بالضغط على enter ، وهناك بعض البيانات المراد كتابتها في المتغير. إذا قام المستخدم فقط بالضغط على الزر enter دون كتابة أي شيء ، فإن `cin` سيستمر في انتظار القيمة.

يمكن ربط عامل الاستخراج `<<` . هنا هو نفس البرنامج كما في المرة السابقة ، ولكن مكتوبة بطريقة أكثر إيجازا:

 `#include<iostream> 
 using namespace std; 
 
 int main() 
 { 
  int a, b; // Variables to hold the two numbers. 
 
  cout << "Please enter two numbers:" << endl; 
  cin >> a >> b; 
  cout << "The sum of your numbers is: " << a + b << endl; 
 } 
` 

عند العمل بالسلاسل ، يقوم مشغل الاستخراج أولاً بقراءة البيانات من `cin` لملء `a` ، ثم قراءة البيانات لملء `b` .

يمكن أيضًا استخدام عبارات printf و scanf القياسية باستخدام c + عن طريق استيراد " ' الملف الاساسي.

## مصادر

1.  http://www.cplusplus.com/reference/ostream/ostream/operator٪3C٪3C/
2.  http://www.cplusplus.com/reference/istream/istream/operator٪3E٪3E/