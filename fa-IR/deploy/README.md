# مرحله منتشر کردن!

> **توجه داشته باشید** که قسمت‌های پیش رو ممکن است کمی سخت به نظر برسد. نا امید نشوید و این بخش را تا آخر ادامه دهید، یکی از مهم‌ترین قسمت‌های توسعه وب سایت منتشرکردن یا Deploy می‌باشد. این فصل در وسط آموزش قرار گرفته است، بنابراین مربی شما می‌تواندبه شما در راه اندازی آنلاین وبسایتتان کمک کند. این به این معنی است که شما می‌توانید به تنهایی ادامه‌ی تمرین خود را به اتمام برسانید حتی اگر زمان کارگاه به پایان برسد.

تا به اینجا وب سایت شما فقط در رایانه شما قابل مشاهده است. حالا شما یاد خواهید گرفت که چگونه آن را دیپلوی کنید! دیپلوی یعنی فرآیند انتشار پروژه شما در اینترنت، تا سایرین بتوانند در نهایت پروژه شما را ببینند. :)

همانطور که یاد گرفتید، وب سایت باید بر یک سرور جای بگیرد. سرورهای زیادی در اینترنت وجود دارد، ما قصد داریم از [PythonAnywhere](https://www.pythonanywhere.com/) استفاده نماییم. PythonAnywhere برای پروژه‌های کوچک که بازدید‌کنندگان خیلی زیادی ندارند رایگان است بنابراین در حال حاضر برای شما مناسب است.

سرویس خارجی دیگری که ما استفاده می‌کنیم [گیت هاب](https://www.github.com) است که سرویس میزبانی کد است. سرویس‌های دیگری نیز وجود دارد، اما تقریباً این روزها همه برنامه نویسان اکانت گیت هاب دارند و الان شما هم خواهید داشت!

این سه مکان برای شما مهم خواهد بود. کامپیوتر محلی شما جایی است که شما در حال توسعه و تست هستید. هنگامی که شما تغییرات را اعمال کردید، یک نسخه از برنامه خود را در گیت هاب قرار می‌دهید. وب سایت شما در PythonAnywhere خواهد بود و شما آن را با یک کپی جدید از کدهای خود که از گیت هاب گرفته‌اید، به روز رسانی خواهید کرد.

# گیت

> ** نکته ** اگر قبلا مراحل نصب را انجام دادید نیازی به انجام این کار وجود ندارد - شما می توانید به بخش بعدی بروید و شروع به ایجاد مخزن یا repository گیت کنید.

{% include "/deploy/install_git.md" %}

## ایجاد مخزن گیت

نرم افزار گیت تغییرات یک مجموعه فایل که در جایی به نام مخزن (به طور مخفف repo) وجود دارند را ردگیری می‌کند. بیایید یکی برای پروژه خودمان بسازیم. کنسول خود را باز کنید و این دستورات را در پوشه `djangogirls` اجرا کنید:

> ** توجه ** قبل از شروع به کار موقعیت پوشه‌ای را که در آن هستید با دستور `pwd` (در سیستم عامل Mac OS X / Linux) یا `cd` (در ویندوز) بفهمید. شما باید در پوشه `djangogirls` باشید.

{% filename %}خط فرمان{% endfilename %}

    $ git init
    Initialized empty Git repository in ~/djangogirls/.git/
    $ git config --global user.name "Your Name"
    $ git config --global user.email you@example.com
    

راه اندازی مخزن گیت کاری است که ما برای هر پرژه فقط یک بار انجام می‌دهیم (لازم نیست مجدداً نام کاربری و ایمیل را وارد کنید).

گیت هاب تغییرات روی تمام فایل‌ها و پوشه های زیرمجموعه این پوشه را پیگیری می‌کند، اما برخی فایل‌هایی که می‌خواهیم آن‌ها را نادیده بگیریم نیز وجود دارند. ما این کار را با ایجاد یک فایل به نام `.gitignore` در پوشه پایه انجام می‌دهیم. ویرایشگر خود را باز کنید و یک فایل جدید با محتویات زیر ایجاد کنید:

{% filename %}.gitignore{% endfilename %}

    *.pyc
    *~
    __pycache__
    myvenv
    db.sqlite3
    /static
    .DS_Store
    

و آن را در پوشه "djangogirls" با نام `.gitignore` ذخیره کنید.

> ** توجه** نقطه در ابتدای نام فایل مهم است! اگر مشکلی در ایجاد آن دارید (به عنوان مثال Mac شما دوست ندارد فایل هایی را بسازید که با نقطه شروع می‌شود)، پس از ویژگی save as استفاده کنید که به کمک آن می‌توانید این نوع فایل‌ها را ذخیره کنید. و مطمئن باشید که هیچ پسوندی مانند `.txt` یا `.py` در انتهای فایل نگذاشته باشید نام این فایل فقط باید `.gitignore` باشد تا توسط Git شناسایی شود.
> 
> **توجه** یکی از فایل‌هایی که در فایل `.gitignore` مشخص شده است فایل `db.sqlite3` است. این فایل پایگاه داده محلی شماست جایی که تمام اطلاعات مربوط به کاربر و پست‌های وبلاگ شما در آن ذخیره می‌شود. ما از روش استاندارد برنامه نویسی استفاده خواهیم کرد به این معنی که ما از پایگاه داده‌های متفاوتی برای توسعه بر روی کامپیوتر محلی و سپس وبسایت اصلی که روی PythonAnywhere هست استفاده خواهیم کرد. پایگاه داده بر روی PythonAnywhere می‌تواند SQLite باشد همانند آنچه بر روی کامپیوتر خود از آن استفاده می‌کنید اما معمولاً از پایگاه داده MySQL برای وبسایت اصلی استفاده می‌کنیم که می‌تواند تعداد بسیار زیاد بازدیدکننده از سایت را مدیریت کند. علاوه بر این حذف کردن فایل SQLite در کپی مربوط به GitHub به این معنی است که تمام پست‌های وبلاگی و superuser هایی که تا الان ساخته‌اید فقط روی کامپیوتر خودتان مورد استفاده خواهد بود و برای محیط اصلی وبسایت باید دوباره آن‌ها را بسازید. شما باید از پایگاه داده محلی خود به عنوان یک زمین بازی خوب استفاده کنید که در آن می‌توانید چیزهای مختلف را آزمایش کنید و نگرانی پاک کردن پست‌های اصلی از وبلاگ را نداشته باشید.

ایده خوبی است که همیشه قبل از زدن دستور `git add` یا هر وقت که مطمئن نیستید چه چیزی تغییر کرده، دستور `git status` را بزنید. این کار کمک می‌کند که از هر نوع غافلگیری مانند اضافه کردن یا commit کردن فایل اشتباه، جلوگیری شود. دستور `git status` اطلاعاتی در مورد فایل‌های ردگیری نشده untracked، اصلاح شده modified، استیج شده staged و نیز درمورد وضعیت شاخه ای که در آن هستیم می‌دهد. خروجی باید شبیه به موارد زیر باشد:

{% filename %}خط فرمان{% endfilename %}

    $ git status
    On branch master
    
    Initial commit
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
            .gitignore
            blog/
            manage.py
            mysite/
            requirements.txt
    
    nothing added to commit but untracked files present (use "git add" to track)
    

و در نهایت ما تغییرات را ذخیره می‌کنیم. به کنسول خود بروید و این دستورات را اجرا کنید:

{% filename %}خط فرمان{% endfilename %}

    $ git add --all .
    $ git commit -m "My Django Girls app, first commit"
     [...]
     13 files changed, 200 insertions(+)
     create mode 100644 .gitignore
     [...]
     create mode 100644 mysite/wsgi.py
    

## کدهای خود را به GitHub انتقال دهید

به [GitHub.com](https://www.github.com) بروید و یک حساب کاربری رایگان برای خود بسازید. اگر این کار را در کارگاه برای اولین بار انجام می‌دهید حواستان باشد که رمز عبور خود را حفظ کنید یا به نر‌م‌افزار مدیریت رمز عبور خود بسپرید.

حالا یک مخزن یا repository بسازید و نام آن را "my-first-blog" بگذارید. گزینه "initialize with a README" را علامت نخورده باقی بگذارید و هم چنین گزینه .gitignore را هم خالی بگذارید (ما بعداً آن را اضافه خواهیم کرد). هم چنین گزینه License را None بگذارید.

![](images/new_github_repo.png)

> **توجه** نام `my-first-blog` مهم است. شما می‌توانید اسم دیگری انتخاب کنید اما از این اسم زیاد استفاده خواهیم کرد و به یاد داشته باشید که اگر اسم دیگری گذاشتید هرجا لازم بود اسم انتخابی خود را استفاده کنید. احتمالاً راحت‌تر است که از همین اسم `my-first-blog` استفاده نمایید.

در صفحه بعد شما URL مخزن خود را خواهید دید که در برخی دستورات بعدی از آن استفاده خواهیم کرد:

![](images/github_get_repo_url_screenshot.png)

حالا وقت آن است که مخزن Git روی کامپیوتر شما را به مخزن موجود در Github وصل کنیم.

خط زیر را در کنسول خود تایپ کنید (`<your-github-username>` را با نام کاربری و گذر واژه خود که در GitHub تعریف کرده اید عوض کنید. علامت‌های کوچکتر و بزرگتر را استفاده نکنید. URL باید دقیقاً همان آدرسی باشد که کمی قبل‌تر دیده‌اید):

{% filename %}خط فرمان{% endfilename %}

    $ git remote add origin https://github.com/<your-github-username>/my-first-blog.git
    $ git push -u origin master
    

وقتی شما فایلی را به GitHub می‌فرستید یا push می‌کنید نام کاربری و گذرواژه از شما پرسیده می‌شود (ممکن است در همان کنسول خط فرمان یا در یک پنجره جدید از شما پرسیده شود) پس از وارد کردن اطلاعات ورود، چیزی شبیه به این خواهید دید:

{% filename %}خط فرمان{% endfilename %}

    Counting objects: 6, done.
    Writing objects: 100% (6/6), 200 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To https://github.com/ola/my-first-blog.git
    
     * [new branch]      master -> master
    Branch master set up to track remote branch master from origin.
    

<!--TODO: maybe do ssh keys installs in install party, and point ppl who dont have it to an extension -->

کد شما الان روی GitHub است. بروید و آن را کنترل کنید! خواهید دید که کدهای شما در جای خوبی است. پروژه [Django](https://github.com/django/django)، دوره آموزشی [Django Girls](https://github.com/DjangoGirls/tutorial) و بسیاری نرم‌افزارهای متن باز فوق العاده دیگر هم، کدهایشان را در GitHub قرار داده‌اند. :)

# تنظیم کردن وبلاگ بر روی PythonAnywhere

## یک حساب کاربری بر روی PythonAnywhere بسازید

> **توجه** شما ممکن است کمی قبل‌تر و در مراحل نصب یک حساب کاربری در PythonAnywhere درست کرده باشید. اگر چنین است نیاز نیست که حساب کاربری دیگری بسازید.

{% include "/deploy/signup_pythonanywhere.md" %}

## وبسایت‌مان را بر روی PythonAnywhere تنظیم کنیم

با کلیک کردن بر روی لوگو و انتخاب گزینه شروع یک کنسول "Bash" به [داشبورد PythonAnywhere ](https://www.pythonanywhere.com/) بروید. این محیط خط فرمان مخصوص PythonAnywhere است، شبیه آنچه در کامپیوتر خود دارید.

![بخش 'New Console' در صفحه وبسایت PythonAnywhere با دکمه‌ای برای 'bash'](images/pythonanywhere_bash_console.png)

> **توجه** PythonAnywhere بر مبنای لینوکس است، بنابراین اگر روی ویندوز کار می‌کنید این محیط خط فرمان با آنچه در ویندوز دارید کمی متفاوت است.

منتشر کردن یک اپلیکیشن تحت وب بر روی PythonAnywhere شامل آوردن کدها از GitHub و تنظیم کردن PythonAnywhere برای تشخیص آن و اجرا کردنش به عنوان یک برنامه تحت وب است. روش‌های غیرخودکار برای این کار وجود دارد اما PythonAnywhere یک ابزار کمکی دارد که همه این کارها را برای شما انجام می‌دهد. اجازه بدهید اول از همه این ابزار را نصب کنیم:

{% filename %}خط فرمان PythonAnywhere {% endfilename %}

    $ pip3.6 install --user pythonanywhere
    

این دستور باید چیزهایی شبیه به `Collecting pythonanywhere` بر روی صفحه نشان دهد و در انتها نیز این پیغام `Successfully installed (...) pythonanywhere- (...)` نمایش داده خواهد شد.

حالا ما برنامه کمکی را اجرا می‌کنیم تا به طور اتوماتیک برنامه ما را از GitHub بخواند. خطوط زیر را در کنسول PythonAnywhere بنویسید (فراموش نکنید که نام کاربری GitHub را به جای `<your-github-username>` بنویسید در نتیجه URL شما مانند URL اختصاصی شما در GitHub میشود):

{% filename %}خط فرمان PythonAnywhere {% endfilename %}

    $ pa_autoconfigure_django.py --python=3.6 https://github.com/<your-github-username>/my-first-blog.git
    

همینطور که به اجراشدن آن نگاه می‌کنید می‌توانید بفهمید که چه کاری انجام می‌دهد:

- دانلود کردن کد شما از GitHub
- ساختن یک محیط مجازی virtualenv بر روی PythonAnywhere شبیه آنچه که بر روی کامپیوتر خود داشتید
- به روزرسانی برخی از تنظیمات شما با تنظیمات مورد نیاز برای انتشار
- تنظیم کردن یک دیتابیس در PythonAnywhere با استفاده از دستور `manage.py migrate`
- تنظیم کردن فایل‌های ثابت شما (بعداً درمورد آن‌ها یاد خواهیم گرفت)
- و در نهایت تنظیم کردن PythonAnywhere برای ارائه اپلیکیشن شما از طریق API خودش

در PythonAnywhere تمام این مراحل اتوماتیک انجام می‌شود اما برای سایر سرورها شما باید دقیقا تمام این اقدامات را انجام دهید.

مهم‌ترین چیزی که اینجا باید به آن توجه کنید آن است که پایگاه داده شما در اینجا از چیزی که بر روی کامپیوتر خود دارید کاملا مستقل است در نتیجه ممکن است اینجا حساب کاربری ادمین یا پست‌های متفاوتی نسبت به کامپیوتر شخصی خود داشته باشید. در نتیجه همان طور که بر روی کامپیوتر خودمان انجام داده ایم باید یک کاربر admin با دستور `createsuperuser` بسازیم. PythonAnywhere به صورت اتوماتیک محیط مجازی یا virtulenv شما را فعال کرده است درنتیجه تنها چیزی که لازم دارید این است که خط زیر را اجرا کنید:

{% filename %}خط فرمان Python Anywhere{% endfilename %}

    (ola.pythonanywhere.com) $ python manage.py createsuperuser
    

مشخصات کاربر ادمین را وارد کنید. می‌توانید این اطلاعات را شبیه اطلاعات ادمین که قبلاً در کامپیوتر خود زده‌اید در نظر بگیرید مگر اینکه بخواهید گذره واژه امن‌تری در PythonAnywhere در نظر بگیرید.

حالا اگر بخواهید می‌‌توانید نگاهی به کدهای خود در PythonAnywhere بیندازید دستور `ls` را بزنید:

{% filename %}خط فرمان PythonAnywhere{% endfilename %}

    (ola.pythonanywhere.com) $ ls
    blog  db.sqlite3  manage.py  mysite requirements.txt static
    (ola.pythonanywhere.com) $ ls blog/
    __init__.py  __pycache__  admin.py  apps.py  migrations  models.pytests.py  static
    templates  views.py
    

علاوه بر این می‌توانید به صفحه File بروید و به کمک مرورگر فایل پیش‌ساخته که در PythonAnywhere قرار داده شده به فایل‌های خود نگاهی بیاندازید. از صفحه کنسول و به کمک کلید منو در گوشه بالا و سمت راست، می توانید به سایر صفحات PythonAnywhere بروید. وقتی شما در یک صفحه هستید، نزدیک به بالای صفحه، لینک‌هایی به سایر صفحات وجود دارد.

## اکنون آنلاین هستید!

وبسایت شما هم اکنون بر روی اینترنت و به صورت عمومی قابل دسترس است! از طریق صفحه "Web" در PythonAnywhere یک لینک به پروژه خود دریافت کنید. شما میتوانید این لینک را با هرکسی که دوست داشته باشید به اشتراک بگذارید :)

> **توجه** این یک تمرین ابتدایی است و ما در هنگام انتشار، برخی میانبرهایی را استفاده کرده‌ایم که از جنبه امنیت وبسایت، روش‌های ایده‌آلی نیستند. If and when you decide to build on this project, or start a new project, you should review the [Django deployment checklist](https://docs.djangoproject.com/en/2.2/howto/deployment/checklist/) for some tips on securing your site.

## نکات عیب‌یابی

اگر شما با خطایی در هنگام اجرا کردن دستور `pa_autoconfigure_django.py` مواجه شدید ممکن است به دلایل زیر باشد:

- فراموشی در ساخت توکن API در PythonAnywhere.
- اشتباه در URL مربوط به GitHub
- اگر خطایی با این مضمون *"Could not find your settings.py"* مشاهده کردید، احتمالاً تمام فایل‌های خود را به Git اضافه نکرده‌اید یا همه آن‌ها را (به کمک دستور push) به GitHub نفرستاده‌اید. به بخش Git در بالا نگاهی دوباره بیندازید
- If you previously signed up for a PythonAnywhere account and had an error with collectstatic, you probably have an older version of SQLite (eg 3.8.2) for your account. In that case, sign up for a new account and try the commands in the PythonAnywhere section above.

اگر هنگام مراجعه به وبسایت خطایی مشاهده کردید اولین جا برای بررسی و عیب یابی نگاه کردن به بخش **error log** است. حتماً در صفحه ["Web"](https://www.pythonanywhere.com/web_app_setup/) در PythonAnywhere لینکی به این بخش پیدا خواهید کرد. نگاه کنید که آیا پیغام خطایی در این صفحه وجود دارد؛ آخرین پیغام‌ها در پایین‌ترین خط ها است.

علاوه بر این دستورالعمل‌های عیب‌یابی عمومی‌تری هم در [صفحه راهنمای سایت PythonAnywhere](http://help.pythonanywhere.com/pages/DebuggingImportError) وجود دارد.

و به یاد داشته باشید که مربی شما اینجاست تا به شما کمک کند!

# وبسایت خود را بررسی کنید!

صفحه اصلی سایت شما باید "It worked" را نشان دهد همانطور که بر روی کامپیوتر خودتان کار می‌کرد. سعی کنید ` /admin/ ` را به انتهای آدرس اینترنتی اضافه کنید و به سایت مدیریت برسید. با نام کاربری و گذرواژه خود وارد شوید خواهید دید که می‌توانید پست جدیدی ایجاد کنید. به یاد داشته باشید که پست‌هایی که در پایگاه داده کامپیوتر خود ایجاد کرده اید بر روی وبسایت آنلاین شما منتقل نشده است.

وقتی چند پست جدید ایجاد کردید به تنظیمات بر روی کامپیوتر خود (local و نه تنظیمات روی PythonAnywhere) برگردید. از اینجا می‌توانید تنظیمات محلی را تغییر دهید. این یک روش رایج در توسعه وبسایت است؛ تغییرات را روی کامپیوتر خود اعمال کنید، آن‌ها را به GitHub بفرستید و سپس این تغییرات را از گیتهاب، بر روی وب سرور کپی کنید. این روش کمک می‌کند که بدون ایجاد خرابی در وبسایت آنلاین بتوان آن را به روز رسانی کرد. جالب نیست؟

یک *خسته نباشید* حسابی به خودتان بگویید! راه اندازی سرور یکی از مهارتی‌ترین بخش‌های توسعه وبسایت است و گاهی برای برخی افراد روزها زمان می‌برد تا بتوانند آن را راه اندازی کنند. اما شما توانستید سایت خود را بر روی اینترنت واقعی راه اندازی کنید!