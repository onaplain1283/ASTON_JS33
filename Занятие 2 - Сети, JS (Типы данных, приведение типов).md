1. Подробно прочитать про метод запроса OPTIONS - и кратко его описать, когда вызывается, где используется, что передает и принимает :

Ответ: Метод OPTIONS запрашивает информацию о доступных способах взаимодействия с сервером, например допустимые методы(они, как правило, приходят с заголовком Access-Control-Allow-Methods), а так же требования необходимые для взаимодействия с сервером. Например в случае с CORS сервер может отправить следующий заголовок - Access-Control-Allow-Origin который сообщает с какого домена можно отправлять запросы на сервер. Обычно посылается браузером когда для дальнейшей работы необходимо отправить запрос на стороний ресурс.

2. Прочитать и описать ключевые особенности "HTTP" Версии 3.0:

Ответ: HTTP3 предостовляет возможность передачи данных с сохранением прежней семантики используя для этого новый транспортный протокол QUIC (вместо TCP) по причине того, что ТСP уже был причиной явных ограничений в межсетевом взаимодействии. Тем самым преимущества HTTP3 сводятся к преимуществам которые даёт QUIC.
Ключевые особенности QUIC следющие:

a. Сокращение фазы установки начального соеденения (рукопожатия) и отсутсвие необходимости при каждом новом подключении делать это заново между уже известными узлами.

b. QUIC так же оперирует потоками и фреймами, в контексте одного потока фрейм является базовой единицой передачи информации, при этом фреймы могут иметь разное предназначение в контексте передачи тех или иных данных. Например HEADERS и DATA фреймы формируют основу HTTP запросов/ответов, а фреймы которые отвечают за передачу метаданных обеспечивающих соеденение в целом передаются в своём отдельном контролирующем потоке. QUIC предостовляет мультеплексирование потоков или проще говоря позволяет создавать несколько независимых потоков, при этом каждая пара запрос/ответ занимает свой отдельный поток и если один поток испытывает проблемы и заблокирован либо имеет потери данных это не влияет на остальные потоки.

с. QUIC также использует новый механизм сжатия заголовков под названием QPACK, который является модификацией HPACK, используемой в HTTP/2. В QPACK заголовки HTTP могут поступать не по порядку и в разных потоках QUIC в отличие от HTTP/2, где TCP обеспечивает упорядоченную доставку пакетов. Чтобы справиться с этим, QPACK использует механизм таблицы поиска для кодирования и декодирования заголовков.

d. QUIC вводит новую концепцию — идентификатор соединения CID. Каждому соединению между двумя конечными точками помимо четырёх основных параметров (ip клиента, ip сервера, порт клиента, порт сервера) присваивается уникальный номер. Поскольку CID определяется на транспортном уровне в самом QUIC, он не меняется при перемещении между сетями. При таком раскладе, даже если один из четырех основных параметров изменится (например при переключении телефона между WIFI и 4g), серверу и клиенту нужно будет просто посмотреть на CID, чтобы узнать старое соединение и дальше использовать его и необходимость в новом рукопожатии исчезает.

e. Представленная в HTTP/2 функция push-уведомлений сервера может рассматриваться как ожидание запроса, который еще предстоит сделать клиенту. Это все еще присутствует в HTTP/3, но его реализация осуществляется через другие механизмы и может быть ограничена. Хотя серверные push-уведомления экономят половину пути туда и обратно, они по-прежнему занимают полосу пропускания. Фрейм PUSH_PROMISE отправляется с сервера через поток запросов, показывающий, что будет содержаться в запросе, на который push будет ответом. Затем он отправляет этот фактический ответ в новом потоке. Отправка сервером может быть ограничена клиентом. Отдельные потоки могут быть отменены с помощью CANCEL_PUSH, даже если ранее это считалось приемлемым.

3. Написать по 2 примера создания примитивных значений (если есть несколько способов - использовать) (string, number, boolean, null, undefined, symbol, bigInt)

string:

    let string = ''
    let string = ""
    let string = ``
    let string = String(value)
    let string = new String(value)

number:

    let number = 1
    let number = Number(value)
    let number = new Number(value)

boolean:

    const good = Boolean(expression)
    const good = Boolean(value)
    const good = new Boolean(expression)
    const good = new Boolean(value)
    const good2 = expression; // Например: let fuzz =  2 > 1

null:

    const foo = null;
    let buzz = null;

undefined:

    let a;
    var a;

Symbol:

    const sym1 = Symbol();
    const sym2 = Symbol("foo");

BigInt:

    const theBiggestInt = 9007199254740991n; // n в конце

    const alsoHuge = BigInt(9007199254740991);

    const hugeString = BigInt("9007199254740991");

    const hugeHex = BigInt("0x1fffffffffffff");// шестнадцатиричная система

4. Почему, если обратиться к переменным созданным через let, const до их объявления - мы получаем ReferenceError?

   https://262.ecma-international.org/14.0/?_gl=1*pfk2ik*_ga*MTE2NTU2MTg3Mi4xNzA1OTk0NDIx*_ga_TDCK4DWEPP*MTcwNTk5NDQyMS4xLjAuMTcwNTk5NDQyMS4wLjAuMA..&_ga=2.107548290.1827252498.1705994421-1165561872.1705994421#sec-let-and-const-declarations

   14.3.1 Let and Const Declarations
   NOTE
   let and const declarations define variables that are scoped to the running execution context's LexicalEnvironment. **The variables are created when their containing Environment Record is instantiated but may not be accessed in any way until the variable's LexicalBinding is evaluated**. A variable defined by a LexicalBinding with an Initializer is assigned the value of its Initializer's AssignmentExpression when the LexicalBinding is evaluated, not when the variable is created. If a LexicalBinding in a let declaration does not have an Initializer the variable is assigned the value undefined when the LexicalBinding is evaluated.

5) Решить:

   const res = "B" + "a" + (1 - "hello");
   console.log(res); // Ответ: BaNaN

   const res2 = (true && 3) + "d";
   console.log(res2); // Ответ: 3d

   const res3 = Boolean(true && 3) + "d";
   console.log(res3); // Ответ: trued
