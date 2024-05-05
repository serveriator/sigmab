# 👁️ سیگما-بی 🏦

سیگما-بی مجموعه ای از پروتکل ها و ابزار های رمزنگاری است که ارائه ***«اثبات خصوصی اندوخته»*** و یا ***«Private Proof of Reserves»*** را برای صرافی های متمرکز رمزارز ممکن می‌کند. «خصوصی» بودن سیگما-بی از درز پیدا کردن آدرس های صرافی و کاربران صرافی و داده های مالی مربوط به صرافی (نظیر مقدار کل بدهی) جلوگیری می‌کند. این سند به فلسفه پشت پروتکل سیگما-بی و جزئیات فنی آن می‌پردازد.

## اثبات اندوخته چیست؟

اثبات اندوخته، صرافی های متمرکز (امانی) را قادر می‌سازد که به کاربران خود اثبات کنند که ***به اندازه بدهی خود به کاربران، اندوخته دارند.*** در پروتکل های اثبات اندوخته فعلی، دو چیز اثبات می‌شود:

1. صرافی به اندازه n واحد پولی اندوخته دارد.
2. مجموع بدهی های صرافی به کاربران از n کوچکتر است.

***برای اثبات قسمت اول***، صرافی ها چاره ای ندارند جز اینکه آدرس کیف پول های خود را بطور عمومی افشا کنند. کاربران می‌توانند با بررسی موجودی داخل این آدرس ها و جمع زدن آنها، مقدار n را بدست بیاورند. **سیگما-بی راه حل نوینی را ارائه می‌کند که صرافی ها بتوانند بدون افشا کردن آدرس های خود، به کاربران ثابت کنند که صاحب n واحد پولی هستند.**

***برای اثبات قسمت دوم***، فرض کنید نوبیتکس لیستی در اختیار دارد که هر سطر آن حاوی شناسه کاربر و موجودی کیف پول امانی او می‌شود. این لیست را «لیست بدهی» می‌نامیم. نوبیتکس می‌تواند این لیست را به طور عمومی منتشر کند. کاربران می‌توانند لیست را مشاهده کرده، و از حضور خود در این لیست مطمئن شوند. پس از اطمینان حاصل کردن از حضور خود در لیست، کاربران می‌توانند مجموع دارایی های همه کاربران در لیست (بدهی کل) را محاسبه کرده و مطمئن شوند که این مقدار، از اندوخته صرافی (مقدار n) کوچکتر است.

- اگر مقدار بدهی ها از مقدار اندوخته ها بزرگتر باشد نوبیتکس واضحا در اثبات اندوخته خود شکست خورده است.
- اگر نام شما در لیست موجود نباشد، بدین معنی است که نوبیتکس بدهی شما را در نظر نگرفته و این احتمال وجود دارد که نوبیتکس به اندازه بدهی خود به کاربران اندوخته نداشته باشد.

*(نکته: کاربران همچنین باید مطمئن شوند که لیست بدهی اعلامی نوبیتکس در یک تاریخ معین، همواره ثابت است و نوبیتکس در هر بار استعلام تغییری در آن ایجاد نمی‌کند. در غیر این صورت نوبیتکس می‌تواند یکبار لیست حاوی نام شما را منتشر کند و بعد از متقاعد کردن شما، نام شما را از لیست حذف کند و نام شخص دیگری را به جای شما گذاشته و او را نیز متقاعد کند)*

## حریم خصوصی لیست بدهی
واضحا انتشار عمومی لیست بدهی ها غیرقابل انجام است چرا که به حریم خصوصی کاربران نوبیتکس آسیب جدی وارد می‌کند. در صورت عمومی شدن لیست بدهی، همه کاربران می‌توانند موجودی رمزارزی همه کاربران را ببینند.

### تابع درهم‌سازی
تابع درهم‌سازی، یک تابع ریاضیاتی است که یک ورودی با اندازه دلخواه می‌گیرد و همواره یک خروجی با اندازه ثابت تحویل می‌دهد. این تابع همچنین ویژگی های زیر را دارد:

- کوچکترین تغییر در ورودی باعث تغییر شگرف در خروجی می‌شود.
- پیدا کردن ورودی از روی خروجی بسیار سخت و ناممکن است.

### تعهد رمزی
با توجه به یک‌طرفه بودن توابع درهم‌سازی امن، آلیس می‌تواند بدون اینکه داده ای را افشا کند، به آن داده متعهد شود. مثال:
فرض کنید آتوسا و بابک میخواهند پشت تلفن «سنگ-کاغذ-قیچی» بازی کنند. متاسفانه همواره این امکان وجود دارد که بابک، در حین اینکه آتوسا انتخاب خود را فریاد میزند، سریعا انتخاب او را شنیده و انتخاب خود را با توجه به انتخاب آتوسا اعلام کند و همواره برنده شود. بابک می‌تواند تاخیر در اعلام انتخاب خود را گردن تاخیر صدا در تلفن بیاندازد.

تابع درهم‌سازی می‌تواند به ما در حل این مشکل کمک کند:

آتوسا و بابک می‌توانند به جای اینکه انتخاب خود را فریاد بزنند، از انتخاب های خود Hash بگیرند و با اعلام این مقدار به یکدیگر، به انتخاب های خود متعهد شوند. پس از رد و بدل کردن تعهد ها، آتوسا و بابک می‌توانند انتخاب اصلی خود را با آرامش کامل اعلام کرده و برنده مشخص می‌شود. همچنین، آتوسا و بابک پس از شنیدن انتخاب های اصلی، می‌توانند با Hash گرفتن از آنها و مقایسه نتیجه با تعهد های قبلی، از پایبند بودن یکدیگر به تعهد های خود مطمئن شوند. در صورت سرپیچی از تعهد ها، بازنده اعلام می‌شود.

### اثبات دانش-صفر
فرض کنید که f تابعی است که چند ورودی میگیرد و یک خروجی می‌دهد. اثبات های دانش-صفر، پروتکل های رمزنگاری هستند که ما را قادر می‌سازند ثابت کنیم ورودی هایی را می‌دانیم که در صورت اعمال f روی آنها، خروجی برابر یک مقدار خاص می‌شود. با استفاده از اثبات های دانش-صفر و تعهد های رمزی، می‌توانیم نوعی «لیست بدهی خصوصی» طراحی کنیم.

### لیست بدهی خصوصی
فرض کنید که بجای انتشار عمومی لیست بدهی، از آن Hash میگیریم و آن را انتشار می‌دهیم. با اینکار به لیست بدهی متعهد می‌شویم. حال فرض کنید که تابع f با مشخصات زیر داریم:

‍‍
$`f(L, i) = (h(L), \sum_{k}{L[k]_{balance}}, L[i]_{id}, L[i]_{balance})`$


این تابع لیست بدهی ($`L`$) و یک اندیس ($`i`$) را به عنوان ورودی دریافت می‌کند و یک چهارتایی را به عنوان خروجی برمی‌گرداند:

- $`h(L)`$ هش لیست بدهی است.
- $`\sum_{k}{L[k]_{balance}}`$ مجموع همه بدهی های موجود در لیست است.
- $`L[i]_{id}`$ شناسه $`i`$-امین کاربر موجود در لیست بدهی است.
- $`L[i]_{balance}`$ موجودی $`i`$-امین کاربر موجود در لیست بدهی است.


حال فرض کنید که نوبیتکس ابتدا لیست بدهی $`L`$ را با توجه به لیست کاربران خود می‌سازد و هش آن را ($`C=h(L)`$) بصورت عمومی منتشر میکند. سپس با استفاده از اثبات های دانش-صفر ثابت می‌کند که ورودی هایی را برای تابع $`f`$ می‌داند که باعث خروجی $`(C,T,K,V)`$ می‌شود. در صورت برابر بودن $`C`$ خروجی با $`C`$ اولیه اعلام شده توسط نوبیتکس، عملا نوبیتکس ثابت کرده است که:

- اولا: مجموع موجودی های کاربران برابر $`T`$ است.
- دوما: شخصی داخل لیست وجود دارد که شناسه او برابر $`K`$ است.
- سوما: موجودی همان شخص داخل لیست برابر $`V`$ است.

آتوسا با دریافت این اثبات و بررسی برابر بودن c با تعهد لیست بدهی ها که نوبیتکس از قبل اعلام کرده بود، قانع می‌شود که هنگام متعهد شدن نوبیتکس به لیست بدهی، آتوسا و ۱۲۳ واحد رمزارز او نیز در نظر گرفته شده اند. همچنین آتوسا متوجه می‌شود که مقدار کل بدهی اعلامی نوبیتکس برابر t است.

آتوسا می‌تواند مقدار t را با مقدار کل اندوخته های نوبیتکس (که n است) مقایسه کند.

## خصوصی سازی اندوخته های نوبیتکس

همانطور که پیش از این گفته شد، نقطه قوت سیگما-بی نسبت به سایر پروتکل ها، قابلیت آن در اثبات اندوخته (قسمت اول) بدون فاش کردن آدرس های صرافی است.

## بلاکچین های Account-based

بیتکوین، به عنوان اولین رمزارزی که تکنولوژی بلاکچین را معرفی کرد، از معماری UTXO پیروی می‌کند. در این معماری، اشخاص، صاحب «حساب» های بیتکوینی نیستند. بلکه صاحبه «سکه» هایی هستند که می‌توانند به سکه های کوجکتر و با صاحب های متفاوت شکسته شوند. در این مدل، یک نفر می‌تواند با شکستن سکه خود به دو سکه کوچکتر، پرداخت بیتکوینی انجام دهد. یکی از این دو سکه باید به نام شخص دریافت‌کننده سکه، و دیگری باقی‌مانده پرداخت و به نام شخص پرداخت‌کننده خواهد بود.

پس از بیتکوین، بلاکچین های دیگری معرفی شدند که از معماری دیگری استفاده می‌کردند: به جای اینکه اشخاص صاحب سکه های با ارزش های متفاوت باشند، هر شخص داخل پروتکل صاحب حسابی است که مقدار موجودی آن با دریافت و پرداخت هایی که انجام می‌دهد تغییر می‌کند. هر حساب نیز به یک کلید عمومی متصل است. 

### لیست موجودی
برخی از بلاکچین های Account-based (مثل اتریوم)، در بلوک های خود، هش کل اکانت های موجود نیز اعلام می‌کنند. این مقدار تحت عنوان stateRoot منتشر می‌شود.

تابع f با مشخصات زیر را در نظر بگیرید:

```
f(i,ethereum_accounts, sig) {
    return (hash(ethereum_accounts), ethereum_account[i].balance, verifySignature(ethereum_accounts[i].pubkey, “I AM NOBITEX”, sig))
}
```

این تابع به عنوان ورودی، کل اکانت های موجود در اتریوم، یک اندیس و یک امضا را دریافت کرده و به عنوان خروجی، هش کل اکانت ها (که برابر با stateRoot می‌شود)، یک موجودی و یک مقدار بولینی (صفر یا یک) را تحویل می‌دهد.

اثبات موفق دانایی ورودی های مناسب برای این تابع بدین معنی است که:

* امضایی را می‌دانیم که نشان می‌دهد صاحب یکی از اکانت های داخل اتریوم هستیم، و مقدار موجودی این اکانت برابر b است.



## TODO
- in mpt path we shoud make public `ECDSACommitmentHash` to be able to chain it with ecdsa circuit
- stealth balance addition currently is only for maximum 2 accounts, we should make it dynamic (addition of n accounts)
