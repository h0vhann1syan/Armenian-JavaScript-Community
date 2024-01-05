# Փոխգործակցությունը բրաուզերների հետ։ alert, prompt և confirm ֆունկցիաները։ Ի դեպ այս ֆունկցիաներն անմիջականորեն կապ չունեն JavaScript ծրագրավորման լեզվի ստանդարտի հետ, այլ բրաուզերի API-ին են պատկանում և նկարագրությունը մանրամասն տրվում է HTML Living Standard-ի մեջ։ Նաև առանց բարդ տերմինների, հնարավորինս մատչելի կբացատրեմ թե ինչ է API-ը:

Քանի-որ **_JavaScript_** ծրագրավորման լեզուն հենց ամենասկզբից ստեղծվել է վեբի ֆրոնտենդ սեգմենտում օգտագործելու համար, նրա ավանդական «աշխատանքային միջավայրը» եղել է բրաուզերը։ Հիմա դա իհարկե այդպես չէ, և ներկայումս **_JavaScript_**-ը կարող է գործարկվել տարբեր պլատֆորմերի վրա, սկսած վեբ սերվերներից մինչև միկրոկոնտրոլերներ։ Բրաուզերի հետ փոխգործակցության համար գոյություն ունեն նրա API-ին պատկանող (_BOM API_) 3 շատ տարածված ֆունկցիաներ՝ _alert_-ը, _prompt_-ը և _confirm_-ը։ Պետք է ասել, որ ռեալ նախագծերի մեջ նրանք քիչ են օգտագործվում, քանի-որ մենք ՉՈՒՆԵՆՔ ՈՐևԷ ՄԻՋՈՑ ՆՐԱՆՑ ԱՐՏԱՔԻՆ ՏԵՍՔԸ ՓՈԽԵԼՈՒ ՀԱՄԱՐ,այն կախված է օգտագործվող բրաուզերի տեսակից։

Օգտագործելով _HTML/CSS/JavaScript_-ի անսպառ հնարավորությունները, կարելի է պատրաստել աչքին շատ ավելի հաճելի, այսպես կոչված փոփափ (_pop-up_) պատուհաններ, և օրինակ կայքի այցելուին փոխանցել ինչ-որ տեղեկատվություն, քան թե նույնը անել ոչ այդքան «բարեհամբույր» տեսք ունեցող _alert_ ֆունկցիայի պատուհանի միջոցով։ Բայց և այնպես գոնե ուսումնական պրոցեսում, կամ որևէ բան արագ թեսթավորելու համար նրանք օգտագործվում են, և վեբ ծրագրավորողը պետք է գերազանց իմանա ինչպես այն կիրառել։ Պլյուս նրանք շատ հուսալի են, և կարելի է ասել, որ պարզությունն այն գինն է, որը մենք վճարում ենք երաշխավորված, հուսալի աշխատանքի դիմաց։

Իսկ հիմա փորձենք հասկանալ ինչ է իրենից ներկայացնում **API**-ը։ Այն _application programming interface_ արտահայտության հապավումն է, որը հայերեն կարելի է թարգմանել որպես կիրառական ծրագրերի ինտերֆեյս։ Եթե հնարավորինս պարզ՝ այն միջոցների ամբողջություն է, որոնց օգնությամբ մի ծրագիրը համագործակցում է մյուս ծրագրի հետ, որևէ համատեղ առաջադրանք կատարելու համար։ Օրինակ վերցնենք էլեկտրական հոսանքի կիրառությունը կենցաղում։ Մենք կարող ենք ընդհանրապես գաղափար չունենալ թե ինչպես և որտեղ է էլեկտրական հոսանքը արտադրվում և ոնց է բաշխվում։ Բայց տան մեջ կան վարդակներ, որոնցից բոլորն են կարողանում օգտվել հեռուստացույց կամ արդուկ միացնելու համար։ Նույն կերպ մենք կարող ենք գաղափար չունենալ թե ոնց է աշխատում հեռուստացույցը, սակայն հեռակառավարման վահանակի օգնությամբ հեշտությամբ միացնում-անջատում կամ ալիքները փոխում ենք։

Նույն սկզբունքով API-ն մեզ հնարավորություն է տալիս պարզեցված տարբերակով աշխատել կողմնակի ծրագրերի հետ, օրինակ կա օպերացիոն համակարգի API, որի օգնությամբ համակարգչային տարբեր ծրագրերը փոխգործակցում են օպերացիոն համակարգի հետ։ Բրաուզերի API-ն հնարավորություն է տալիս **_JavaScript_** ծրագրավորման լեզվի միջոցով շատ հեշտ կատարել գործողություններ, որոնք իրականում տակից շատ բարդ են։ Այն չափազանց հեշտացնում է ծրագրավորողի աշխատանքը։

Օրինակ _Geolocation API_-ն տրամադրում է օգտագործման համար շատ պարզ կառուցվածքներ, որոնց օգնությամբ մենք կարող ենք հեշտությամբ աշխատել գտնվելու վայրի մասին տվյալների հետ, և ասենք թե _Google Map_-ի վրա նշել մեր տեղը։ Բայց իրականում բրաուզերի մեջ այդ ժամանակ կատարվում է բարդ, համեմատաբար ցածր մակարդակի կոդ (_կարող է լինել օրինակ C++ լեզվով_), որը պատասխանատու է GPS-ի միացման, տվյալները ստանալու, դրանք մշակելու, համակարգելու և բրաուզերի մեջ աշխատող մեր ծրագրին հաղորդելու համար։

Մինչ _alert_-ին, _prompt_-ին և _confirm_-ին անդրադառնալը, բացատրեմ ևս մի տերմին, որը հաճախ է օգտագործվում և անմիջականորեն վերաբերում է այդ 3 մեթոդներին։ Մոդալ պատուհաններ (_Modal window_) կոչվում են այն դիալոգային պատուհանները, որոնք արգելափակում են մնացած ողջ ինտերֆեյսի օգտագործման հնարավորությունը, քանի դեռ պատուհանը չենք փակել։

Եվ այսպես սկսենք **alert**-ից։ Սինթաքսը հետևյալն է՝

window.alert(message)

Կարող ենք կանչել նաև առանց _window_ գլոբալ օբյեկտն օգտագործելու, ուղղակի

alert(message)։

- message պարամետրը ոչ պարտադիր է, այն օգտագործվում է կայքի այցելուին ինչ-որ հաղորդագրություն ցույց տալու համար։ Այցելուն չի կարող բացի այդ հաղորդագրությունը հաստատելուց, ուրիշ որևէ բան անել։ Քանի որ պատուհանը նաև մոդալ է, այցելուն քանի դեռ չի հաստատել որ հաղորդագրությունը տեսել է, այսինքն քանի դեռ OK կոճակը չի սեղմել, նա կայքում ուրիշ ոչ մի բան անել չի կարող։ Նշեմ նաև, որ alert-ը բոլոր այլ տիպի տվյալները փոխակերպում է _String_ տիպի, նոր արտածում։

**prompt**-ը բացում է մոդալ պատուհան, որտեղ կա տվյալների մուտքագրման համար դաշտ և ոչ պարտադիր հանդիսացող տեքստի մուտքագրման հարցում։ Սինթաքսը հետևյալն է՝

result = window.prompt(message, default);

Կարող ենք օգտագործել նաև կարճ տարբերակը, առանց window գլոբալ օբյեկտի։

result = prompt(message, default);

- result-ը դա փոփոխական է, որն իր մեջ պահում է կայքի այցելուի կողմից մուտքագրված տեքստը (String տիպ), կամ null։

- message-ն այն տեքստն է, որը ցուցադրվում է պատուհանի մեջ։ Այն ոչ պարտադիր պարամետր է։

- default-ը սկզբնական արժեքն է, և մուտքագրման դաշտում երևում է։ Հենց այցելուն սկսում է ինչ որ տեքստ հավաքել, default-ի արժեքը անհետանում է։ Այս պարամետրը ցանկալի է տալ, թեկուզ և դատարկ չակերտների տեսքով, որովհետև դրա բացակայության ժամանակ մեր շատ սիրելի internet explorer-ի հին տարբերակները մուտքագրման դաշտում արտածում են undefined, ինչը համաձայնեք՝ տգեղ է։

Այսպիսով երբ սեղմում ենք _OK_ կոճակը, ապա ֆունկցիան վերադարձնում է այն տեքստը, որը մուտք է արվել մուտքագրման դաշտում։ Երբ սեղմում ենք _OK_ կոճակը, սակայն առանց որևէ տեքստ մուտք անելու, ապա վերադառնում է _default_ պարամետրում նշված արժեքը, կամ դատարկ տող, եթե տվյալ պարամետրը տրված չէ։ Եվ վերջապես,երբ սեղմում ենք _Cancel_ կոճակը, ապա ֆունկցիան վերադարձնում է _null_:

**confirm**-ը բացում է մոդալ պատուհան, որն ունի երկու կոճակ՝ (_OK և Cancel_), ինչպես նաև ոչ պարտադիր հանդիսացող տեքստային հաղորդագրություն։ Սինթաքսը հետևյալն է՝

result = window.confirm(message)

Կարող ենք օգտագործել կարճ գրելաձև, բաց թողնելով window գլոբալ օբյեկտը։

result = confirm(message)

- message - Ոչ պարտադիր տեքստային հաղորդագրություն, որը կարտածվի դիալոգային պատուհանի մեջ։
- result - Բուլյան արժեք (_true կամ false_), որը արձանագրում է թե որ կոճակն է սեղմվել (_true-ն դա OK-ի դեպքում, false-ը՝ Cancel-ի_):