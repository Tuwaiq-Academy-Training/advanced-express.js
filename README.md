
محتوى الملف:
- ماهو json
- الخصائصRequest
- دوال Response


## ماهو json

ال JSON أو JavaScript Object Symation هي صيغة بسيطة وقابلة للقراءة بسهولة من قبل الإنسان وتستخدم لتمثيل البيانات و تبادلها بين الأنظمة البرمجية المختلفة.

جيسون JSON ليست لغة برمجية إنما هي طريقة متفق عليها بين لغات البرمجة المختلفة لتمثيل البيانات بهدف سهولة تبادل البيانات بين هذه اللغات.

صيغة جيسون تمثل عن طريق نص، والبنية لهذا النص تشبه الكائن أو Object في لغة البرمجة جافاسكربت, وهذه الصيغة مدعومة من لغات البرمجة الأساسية الأخرى وتستخدم هذه الصيغة بشكل كبير لتبادل البيانات بين الخادم والعميل Client-Server.

####  كيفية تمثيل البيانات 

الجزءان الأساسيان اللذان يشكلان JSON هما المفاتيح Keys والقيم Values.

- المفتاح Key : يمثل اسم فريد لقيمة البيانات ويتم وضعه عادة بين علامات التنصيص

- القيمة Value : تمثل البيانات ويمكن أن تمثل اكثر من نوع بيانات مثل النصوص والأرقام والمصفوفات.

معًا يشكل Key / Value سطر في صيغة جيسون حيث يتم استخدام علامة , كفاصل بين السطور.

#### أنواع البيانات للقيم في JSON

- ال Array المصفوفة: مجموعة من القيم المترابطة على سبيل المثال: رواتب الموظفين ويتم تمثيلها كالتالي [2000, 5000,6000].

- ال Boolean قيمة منطقية: ولها احتمالان True او False.

- ال Number رقم: تكون القيمة عبارة عدد صحيحا أو حقيقيا أو فواصل عشرية.

- ال Object لكائن: مجموعة مترابطة من أزواج من المفاتيح / القيم Key / Value.

- ال String السلسلة النصية: مجموعة من الأحرف النصية العادية تشكل عادة كلمة.



## Request

### مقدمة في مفهوم req.params
-َ params هي اختصار لكلمة parameters وهي property خاصة بrequsts والتي من خلالها يمكننا الحصول على القيم المرسلة في الرابط ، لنوضح ذلك بمثال: نفترض لدينا قائمة بالطلاب الجامعيين ولعرض معلومات الطالب نحتاج لمعرفة رقمه الجامعي وللوصول له نستخدم params كما موضح أدناه :


محتوى ملف `app.js`:


     let students =[{id:1,name:'Ahmed',age:22,gpa:4.03}, {id:2,name:'Salem',age:21,gpa:3.83}, {id:3,name:'Khaled',age:23,gpa:4.52}, {id:4,name:'Ali',age:22,gpa:2.98}, {id:5,name:'Nasser',age:21,gpa:3.74}] 
     app.get ('/students/:id', function(req,res){ 
     let studentId = req.params.id
     console.log(studentId)
     if(0<studentId<students.length){
     student=students[studentId-1]
     res.locals.student=student
    res.render( 'show', student)}
    else
    res.render( 'errorMessage')})
    
    
    
 ##  ملاحظة: 
 إذا كنت تريد إرسال قيمة فالرابط فيجيب عليك وضع نقطتان رأسيتان قبل اسم الخاصية كما في المثال أعلاه تم وضع نقطتان رأسيتان قبل id في الرابط  'students/:id/'  في حين الإرسال تستبدل id:  برقم الطالب الجامعي  'students/3/'  كما موضح أدناه.
    
     http://localhost:3000/students/3
    
    
    
## خاصية req.body

قبل الدخول في تفاصيل العملية، لنقم أولاً بتجزئتها وفهمها، فالجزء الأول req هو إختصار request أي الطلب.
والجزء الثاني body أي المحتوى. نستنتج من ذلك أن req.body تعني المحتوى لهذا لطلب.

هذه العملية تمكننا من الوصول الى محتوى الطلب وتحديد المتغير أو القيمة المرسلة مع الطلب وإستخدامها.
مثال، في حالة قام أحد المستخدمين بإرسال طلب للوصول الى معلوماته الشخصية، ستقوم العملية بإرسال 
المعرف id لهذا المستخدم كجزء من محتواها. وعند وصول الطلب سيتم التحقق من المستخدم من ثم إرسال
البيانات الخاصة به لعرضها.


- مثال إستخدام req.body للوصول الى id المستخدم : 


       const app = require('express')()

       app.use(bodyParser.json()) 
       app.use(bodyParser.urlencoded({ extended: true })) 

       app.post('/userInfo', function (req, res) {
       let userID = req.body.id;// we accesed user's id by using req.body
         })
         
         
 ## خاصية req.headers

كائن يحتوي على رأس محدد مسبقًا / مخصص مقدم في الطلب الحالي.

#### طريقة الاستعمال

ال req.headers;
 
غالبًا ما نريد التحقق من رؤوس الطلب الحالي. يمكن القيام بذلك بسهولة في الأشرعة.



         
        
 ## مقدمة في مفهوم ()res.send:

يتم إرسال رد عن طريق استدعاء دالة ()res.send تتكون هذه الدالة من جزء واحد فقط وهو body يمثل الرد الذي سيتم ارساله وقد يكون الرد أيًا مما يلي: 


- Buffer.
- String.
- Object.
- Array.

##  عمليه res.json
 
 وهي عمليه متعلقه بإرسال رد من نوع json عن طريق استدعاء داله res.json ، وتقبل json انواع بيانات محدده وهي 

- string 
- number 
- boolean
- array
- objects
- null




## المرجع 
https://expressjs.com/en/4x/api.html#express
