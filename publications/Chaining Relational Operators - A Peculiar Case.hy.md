# JavaScript-ի զվարճալի տարօրինակությունները շարքից: Մաս 4

**JavaScript** ծրագրավորման լեզվի զվարճալի տարօրինակություններին անդրադառնալու առիթներ արդեն մի քանի անգամ եղել է։ Մի խումբ էնտուզիաստներ նույնիսկ [կայք](https://wtfjs.com/?fbclid=IwAR0CBxkPEzmbR58rEOKjgS8hd5YDJ8MAXhWMBC2P6rmUkg3GDdxHtDRPl3o) են ստեղծել, որտեղ ըստ տարեթվերի շատ կոկիկ դասավորել են տասնյակներով նման զվարճալի օրինակներ:

Սակայն ազնվության համար նշենք, որ դրանք իրականում տարօրինակություններ չեն, միգուցե զվարճալի են, բայց ամբողջովին տեղավորվում են **JavaScript** ծրագրավորման լեզվի դավանած փիլիսոփայության մեջ։ Լեզուն չափազանց հանդուրժող է տարբեր տիպերին պատկանող արժեքների օգտագործմամբ՝ երբեմն նույնիսկ անհեթեթության հասնող օպերացիաների նկատմամբ, երբ որևէ տեղ սպասում է որևէ տիպի արժեք, սակայն ստանում է ոչ այն, ինչ սպասում էր, չի դադարեցնում ծրագրի աշխատանքը, այլ փորձում է տիպերի անուղղակի վերափոխումների արդյունքում ստանալ հնարավորինս կոռեկտ արժեք, և շարունակել ծրագրի աշխատանքը։ **JavaScript** ծրագրավորման լեզվի որդեգրած թույլ տիպաբանության կոնցեպցիան ո՛չ լավ է, ո՛չ վատ։ Այն իհարկե լեզվին տալիս է անսահման ճկունություն՝ անհասանելի ծրագրավորման լեզուների ճնշող մեծամասնության համար, երբեմն օգնում է կրճատել գրվող կոդի ծավալը, սակայն մյուս կողմից էլ չափազանց բարձրացնում է ծրագրի անկանխատեսելի վարքագիծ դրսևորելու ռիսկը, ստիպում է կոդում մեծացնել ստուգումների քանակը, թեսթավորումը դարձնում է ավելի բարդ և ժամանակատար։ Իսկ հիմա դիտարկենք մի քանի չափազանց հետաքրքիր, զվարճալի տարօրինակություններ.

```js
1 < 2 < 3; // true
3 > 2 > 1; // false
```

Իրականում վերևի առաջին օրինակում ամեն ինչ շատ պարզ է։ Համեմատության օպերատորները վերադարձնում են Բուլյան արժեք՝ _true_ կամ _false_: Երբ արտահայտությունը նայում ենք ձախից աջ, ապա արտահայտության առաջին մասը՝ _1 < 2_, վերադարձնում է _true_: Ապա արտահայտության երկրորդ մասում՝ _true < 3_, նույնպես վերադառնում է _true_, որովհետև փորձելով համեմատել Բուլյան արժեք հանդիսացող _true_-ն _3_ թվի հետ, համեմատության օպերատորը _true_-ն անուղղակի վերածում է թվի, և ստանում _1_։ Ինչպես հիշում ենք տիպերի անուղղակի վերափոխումները դասից, Բուլյան _false_-ը թվային արժեքի վերափոխվելիս դառնում է _0_, իսկ _true_-ն՝ _1_։

Երկրորդ օրինակը նույնպես փորձենք քայլ առ քայլ նայել։ _3 > 2_ համեմատությունը վերադարձնում է _true_, ապա կատարվում է հաջորդ համեմատությունը՝ _true > 1_, որն էլ վերադարձնում է _false_, քանի-որ ինչպես նշեցինք, Բուլյան _true_ արժեքի թվային վերափոխման ժամանակ ստանում ենք _1_, իսկ _1_-ը _1_-ից չի կարող մեծ լինել, նրանք հավասար են, այդ իսկ պատճառով ամբողջ արտահայտությունը վերադարձնում է _false_:

```js
console.log([1, 2, 3] + [4, 5, 6]); // 1, 2, 34, 5, 6
```

Այստեղ + օպերատորը հանդես է գալիս ոչ թե մեզ քաջ հայտնի թվաբանական գումարման, այլ որպես _String_ տիպի հետ աշխատելու համար նախատեսված համակցման (_concatenation_) օպերատոր։ Իսկ համակցման օպերատորն արտահայտության ձախ և աջ կողմերում գտնվող զանգվածներն ուղղակի վերափոխում է տողային տիպի, և միացնում իրար։ Այսինքն այս «գումարման», իրականում՝ համակցման արդյունքը պատկանում է _String_ տիպի։ Եթե այդ արտահայտության արդյունքը վերագրենք որևէ փոփոխականի, և _typeof_ օպերատորով ստուգենք, կարող ենք դրանում համոզվել։

```js
parseInt("fack", 16); // 4012
```

Ի՞նչ է կատարվում այստեղ։ Նախ վերհիշենք, թե ինչպես է աշխատում **parseInt** ֆունկցիան։ Սինթաքսը հետևյալն է՝

`parseInt(string, radix)`;

Որտեղ `string` պարամետրն այն արժեքն է, որից ֆունկցիան պետք է ստանա, առանձնացնի թիվը։ Արգումենտ տալու ժամանակ տողի սկզբի բացատներն անտեսվում են։ Եթե արգումենտը չի պատկանում _String_ տիպի, ապա տակից կատարվող աբստրակտ _toString_ օպերացիայի արդյունքում այն այնուամենայնիվ վերածվում է տողի։

`radix` պարամետրը _2-ից 36_ միջակայքում գտնվող ամբողջ թիվ է, և ֆունկցիային հուշում է, թե մենք ինչպիսի հաշվարկման համակարգ ենք ուզում օգտագործել։ Որպես սկզբնական արժեք ընդունված է տասական համակարգը, բայց սպեցիֆիկացիան խորհուրդ է տալիս անգամ տասական հաշվարկման համակարգն օգտագործելիս անպայման այն նշել, քանի-որ որոշ միջավայրերում (_Օրինակ բրաուզերների հին տարբերակներում, որոնք ինչքան էլ զարմանալի թվա, դեռևս միլիոնավոր օգտագործողներ ունեն_) կարող են սխալների պատճառ դառնալ։

Այժմ դիտարկենք մեր օրինակը։ Ինչպես տեսնում ենք որպես երկրորդ արգումենտ (_radix_) նշված է _16_ թիվը, սա նշանակում է, որ մենք որպես հաշվարկման համակարգ ուզում ենք լինի տասնվեցական (_Hexadecimal_) համակարգը։ Այն ինչպես գիտենք բաղկացած է _0-9_ թվանշաններից և լատինական այբուբենի _A-F_ տառերից։ Այսինքն այս համակարգում _9_-ից հետո գալիս է _A_-ն, հետո _B_-ն և այդպես մինչև _F_, որի համարժեքը տասական համակարգում _15_ թիվն է։

Եվ այսպես ֆունկցիան սկսում է կարդալ _"Fack"_ տողը, փորձելով այնտեղից տասնվեցական հաշվարկման համակարգի տրամաբանությամբ թիվ ստանալ։ Այդ համակարգում _"F"_ տառը օգտագործվում է, ֆունկցիան անցնում է առաջ, _"a"_ տառը նույնպես իմաստ ունի, ֆունկցիան շարունակում է աշխատանքը հասնելով _"c"_ տառին, որը կրկին տասնվեցական համակարգում օգտագործվում է։ _"k"_ տառ տասնվեցական հաշվարկման համակարգում չկա, այստեղ ֆունկցիան դադարեցնում է իր աշխատանքը, և վերադարձնում _"Fac"_ տողի տասական համակարգում համարժեքը՝ որը _4012_ թիվն է:

Ի դեպ նկատենք, որ այս բոլոր այսպես կոչված «տարօրինակություններն» իրականում ամբողջությամբ օրինաչափ վարքագիծ է, որը բխում է _JavaScript_ ծրագրավորման լեզվի ոգուց և փիլիսոփայությունից։ Եվ լեզվի ստանդարտին մանրամասն ծանոթանալուց հետո մենք հասկանում ենք, որ այն ոչ թե տարօրինակ, այլ չափազանց **ՅՈՒՐՕՐԻՆԱԿ, ԻՆՔՆԱՏԻՊ, ՃԿՈՒՆ և ՀՐԱՇԱԼԻ լեզու է**, արժանի սիրո և ուշադրության։