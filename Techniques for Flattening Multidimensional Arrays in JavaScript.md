# Անհրաժեշտ է ստեղծել ֆունկցիա, որը որպես արգումենտ կստանա բազմաչափ զանգված և կվերադարձնի նոր միաչափ զանգված՝ բաղկացած բազմաչափ զանգվածի բոլոր ներդրվածության մակարդակներում գտնվող էլեմենտներից:

Նախ բերեք վերհիշենք թե ինչ են իրենցից ներկայացնում բազմաչափ զանգվածները։ **JavaScript**-ում զանգվածի էլեմենտները կարող են լինել ցանկացած տիպի՝ թվային, տողային, Բուլյան և այլն։ Բնականաբար էլեմենտները կարող են լինել նաև բարդ օբյեկտային տիպին պատկանող զանգվածներից, և այս դեպքում մենք կունենանք զանգվածների զանգված՝ ինչպես ընդունված է ասել երկչափ զանգված կամ մատրիցա։ Ոչինչ չի խանգարում, որպեսզի զանգվածի էլեմենտ հանդիսացող զանգվածը նույնպես բաղկացած լինի զանգվածներից, այս դեպքում մենք կունենանք եռաչափ զանգված և այդպես շարունակ:

Խնդիրը կայանում է նրանում, որպեսզի մենք ստեղծենք այնպիսի ֆունկցիա, որը որպես արգումենտ կստանա երկչափ, եռաչափ, կամ ուղղակի ասենք բազմաչափ զանգված, և կվերադարձնի նոր, սովորական միաչափ զանգված, որը բաղկացած կլինի բազմաչափ զանգվածի բոլոր ներդրվածության մակարդակներում գտնվող էլեմենտներից։ Խնդրի լուծման տարբերակներն իհարկե շատ են, մենք կդիտարկենք երկու տարբերակ՝ ռեկուրսիայի կամ զանգվածի պրոտոտիպում ներդրված flat() մեթոդի օգնությամբ։ Եվ այսպես՝ առաջին տարբերակը՝ ռեկուրսիայի օգնությամբ․

```
function flat(arr) {
    let res = [];
    arr.forEach((item) => {
        if (Array.isArray(item)) {
            res = res.concat(flat(item));
        } else {
            res.push(item);
        }
    });
    return res;
}
```

Այժմ քայլ առ քայլ տեսնենք թե ինչպես է ֆունկցիան աշխատում։ Ֆունկցիան պետք է վերադարձնի նոր զանգված, և մեզ անհրաժեշտ է հայտարարել _res_ նախնական դատարկ զանգվածը։ Ապա արգումենտով ստացված _arr_ բազմաչափ զանգվածի վրա կանչում ենք զանգվածների _forEach_ մեթոդը։ Անցնելով զանգվածի յուրաքանչյուր էլեմենտի վրայով, _Array.isArray_ մեթոդով ստուգում ենք այն իրենից զանգված է ներկայացնում թե ոչ։ Եթե այն նորից զանգված է, ապա նրա վրա կրկին կանչում ենք _flat_ ֆունկցիան, եթե ոչ՝ ֆունկցիայի մարմնում ստեղծված _res_ զանգվածի մեջ վերջից ավելացնում ենք այդ էլեմենտը։ Ֆունկցիան վերադարձնում է _res_ զանգվածը, որն էլ արդեն միաչափ զանգված է՝ բաղկացած _arr_ բազմաչափ զանգվածի բոլոր ներդրվածության մակարդակներում գտնվող էլեմենտներից: Այժմ կանչենք ֆունկցիան, և նրան տանք որևէ բազմաչափ զանգված, տեսնելու համար թե արդյոք այն ճիշտ է աշխատում․

```
flat( [1, 2, 3, [4, 5, 6, [7, 8, 9]]] ); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Դիտարկենք երկրորդ տարբերակը։ Զանգվածի պրոտոտիպի մեջ կա ներդրված **flat** մեթոդը։ Սինթաքսը հետևյալն է՝

```
const newArray = arr.flat(depth)։
```

Մեթոդը վերադարձնում է _newArray_ նոր զանգվածը, որտեղ _arr_ զանգվածի մեջ գտնվող «ենթազանգվածները» բարձրացվում են մինչև _depth_ արգումենտում նշված մակարդակին։ _depth_ պարամետրը ոչ պարտադիր (_օպցիոնալ_) է։ Եթե մենք այնտեղ ոչինչ չգրենք, ապա որպես նախնական արժեք այն կընդունի _1_-ը։ Որպեսզի մեթոդը անկախ զանգվածի ներդրվածության մակարդակից (_երկչափ, եռաչափ և այլն_), միշտ վերադարձնի միաչափ զանգված, կարելի է _depth_ պարամետրին տալ _Infinity_ արժեքը։ Օրինակ՝

```
[1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]].flat(Infinity); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

Փոփոխելով _depth_ արգումենտի արժեքը, մենք կարող ենք կարգավորել մեթոդի աշխատանքը, ստիպելով նրան վերադարձնել նոր զանգված մինչև այնքան ներդրվածության մակարդակով, ինչքան որ մեզ անհրաժեշտ է: Մեթոդի մասին ավելի մանրամասն կարելի է ծանոթանալ [այստեղ](https://tc39.es/proposal-flatMap/#sec-Array.prototype.flat):