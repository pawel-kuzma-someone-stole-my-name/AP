-  Generalnie temat jest bardzo obszerny, i każdy typ API zasługuje na oddzielne spotkanie. W tej prezentacji po krutce i po łebkach powiem o
   -  co to jest API i jego rodzajach
   -  po to aby zbydować tło
   -  żebyśmy lepiej zrozumieli czym jest REST

#index
Wydaje mi się, a przynajmnij ja tak mam, miałem, że w sytuacji gdy ktoś pyta się mnie co to jest API, to moim pierwszym skojarzaniem jest o API RESTowym 	

#2
####API
API kontroluje wszystkie punkty dostępowe aplikacji. Do tych aplikacji można wysłać zewnętrzne żądanie, które to API obsługuje jako tłumacz. To właśnie Interfejs Programowania Aplikacji prześle zapytania do aplikacji oraz pozwoli odesłać jej informację zwrotną.

#3
####API
API to bardzo szerokie pojecie, pod tym terminem kryją się nie tylko webowe API, ale i pulpit w systemie sam w sobie oraz biblioteki

#6
####RPC
Teraz omówimy po krótce najpopularniejsze rodzaje API wykorzystywanane w szeroko pojętym web developmencie

#7
####RPC
Nazwa same przez siebie definiuję czym dokładnie jest ten styl architektoniczny. Wywołujemy zdalne funkcję / procedurę, zamiast lokalnie to za pomocą protokołu HTTP. Będę tutaj czepliwy gdyż teoretycznie funkcja jest bytem (podprogramem) który ma wejście i wyjście, zaś procedura nie zwraca nic, zmienia stan globalny. W tym podejściu API jednak możemy oczekiwać na odpowiedzi od API.

#9
####SOAP
Został zaprojektowany tak, aby aplikacje zbudowane w różnych językach i na różnych platformach mogły się komunikować. 
Narzuca wbudowane reguły, które zwiększają jego złożoność i obciążenie, co może prowadzić do dłuższych czasów ładowania strony / przetważania.

#16
####REST VS RESTFULL
Z kąd takie porównanie? Przegrzebując internet napotykałem często na te 2 pojęcia i pamiętam jak początkowo myślałem, że są to 2 różne rzeczy, stack overfow był lekko zaśmiecony na ten temat i nie potrafiłem zrozumieć różnicy pomiędzy tymi pojęciami. Ludzie też nie pomagali z racji tego, że ludzie urzywają tych pojęć zamiennie i ja jako świeżam - przez to nie rozumiałem o do mnie mówią

#17
####GENEZA
Roy Fielding w 2000 napisał pracę doktorancką gdzie zaprezentował wzorzeć REST (link do pracy a sam RESTA jest opisany w 5 rozdziale)

#18 
####CECHY I
Aby architektóre nazwać RESTową musi ona spełniać pewne założenia

#19
####CECHY II
Pojęcie sesji czy stanu użytkownika w architekturze REST nie ma miejsca. Requesty nie może być zapamiętany

#20
####CECHY III
Expires – data wygaśnięcia danych. Kiedy termin upłynie, zasób musi zostać pobrany z serwera i może być ponownie zapamiętany.
Cache-Control – definiuje czy zasób powinien być zapamiętany oraz na jak długo.
ETag – unikalny identyfikator / token, bezpośrednio powiązany z zapamiętanym zasobem. Zmienia się w momencie aktualizacji wartości.
Last-Modified – określa, kiedy zasób został zaktualizowany / zmodyfikowany.

#23
#####CECHY powodują, że

#24 
####Model dojrzałości
Tak więc, omówiliśmy sobie suchą teorie RESTa. Jak to wygląda w prawdziwym świecie?

Wiele serwisów łamie zasady w taki czy inny sposób, ale nadal potocznie określa się je mianem RESTowymi. Dlatego Leonard Richardson stworzył model, który dzieli REST na poziomy zgodności.

#25
####Model dojrzałości
Zazwyczaj model ten jest przedstawiany jako piramida gdzie 0 jest na samym dole zaś 3 na górze.

####0
####SWAMP Bagno POX (Plain Old XML)
oznacza, że używasz HTTP do tunelowania informacji. Poziom dojrzałości zero nie korzysta z żadnych funkcji URI, http i HATEOAS.
ALE MIMO TO API POWINNO PRZESTRZEGAĆ PEWNYCH REGUŁ (O TYM PÓŹNIEJ) 

lista reguł:
1
Aby URI były łatwe do skanowania i interpretowania przez ludzi, używaj znaku myślnika (-) w celu poprawy czytelności nazw w długich segmentach ścieżek. Wszędzie tam, gdzie w jakimkolwiek języku użyto by spacji lub myślnika, należy użyć myślnika w URI.

2
Aplikacje przeglądające tekst (przeglądarki, edytory, itp.) często podkreślają URI, aby zapewnić wizualną wskazówkę, że są one klikalne. W zależności od czcionki aplikacji, znak podkreślenia (_) może być częściowo przesłonięty lub całkowicie ukryty przez to podkreślenie.

3
Trudno było mi znaleźć konkretny powód, w specyfikacji znalazłem informację, że tak powinno być 😊 od strony klienta nie ma to znaczenia, ale dla niektórych serwerów może mieć np. dla IIS nie ma to znaczenia ale dla Apache już tak.

4
Interfejs API REST nie powinien zawierać sztucznych rozszerzeń plików w URI, aby wskazać format treści wiadomości. Zamiast tego, powinny one polegać na typie mediów, przekazywanym za pomocą naglówka Content-Type, aby określić, jak przetwarzać zawartość ciała.

####1 Zasoby
 Zasoby to podstawowe fragmenty danych, na których działa aplikacja. Będą one często odpowiadać modelom w aplikacji. Projektowanie interfejsów API na poziomie 1 polega na używaniu różnych adresów URL do interakcji z różnymi zasobami w aplikacji. 

lista reguł:
2
Jest to jedna z najważniejszych zasad do przestrzegania, ponieważ ostatni znak w ścieżce URI, ukośnik (/) nie dodaje żadnej wartości semantycznej i może powodować zamieszanie. Interfejsy REST API nie powinny oczekiwać ukośnika końcowego i nie powinny zawierać ich w linkach, które dostarczają klientom. To jest tak jak ktoś coś ci powiada / mówi i kończy zdanie słowem więc, huj wie czy się czegoś spodziewać czy będzie kontynuował swoje przemyślenia dalej

4
Przeszukując Internet napotkałem się na wiele przykładów gdzie jest użyta liczba mnoga jak i liczba pojedyncza – osobiście nauczono mnie aby była to liczba mnoga, którą stosuję – generalnie co byś nie wybrał BĄDŹ KONSEKWENTY

#2
#### CZASOWNIKI HTTPS
 Dzięki czasownikom HTTP mamy dostęp do tego samego zasobu / adresu, ale winnym kontekście. Jeśli chcemy uzyskać listę stron, wysyłamy żądanie GET do /pages, ale jeśli chcemy utworzyć nową stronę, używamy POST do /pages

#3
#### Hypermedia as the engine of application state (HATEOAS)
Negocjacje treści koncentrują się na różnych reprezentacjach konkretnego zasobu. Negocjacja treści ogólnie rzecz biorąc, to wysłanie przez klienta prośby aby zwrócony zasób był odpowiednio sformatowany. 
HATEOAS dotyczy wykrywalności działań na zasobie, inaczej mówiąc dodawanie do response danych które odkrywają klientowi część lub całość API.
Zapewnia on łatwość nawigacji po zasobie i dostępnych w nim akcjach. W ten sposób klient nie musi wiedzieć, jak wchodzić w interakcję z aplikacją w celu wykonania różnych akcji, ponieważ wszystkie metadane będą zawarte w odpowiedziach serwera.

accept:
Accept: application/json - klient chce otrzymać odpowiedź w formacie JSON. Zadaniem serwera jest teraz określenie, czy może on zwrócić taką reprezentację.
Jeśli serwer nie może zwrócić JSON, musi poinformować o tym klienta. Służy do tego kod stanu 406 Not Acceptable: idealnie byłoby, gdyby serwer wskazał również, jakie typy mediów może zwrócić; nie jest jednak do tego zobowiązany. Może to zrobić za pomocą Content-Type w odpowiedzi.

content-type:
Drugim aspektem negocjacji zawartości jest identyfikacja przychodzącego nagłówka Content-Type i określenie, czy serwer może deserializować te dane.

#26
Wiele serwisów, które potocznie nazywamy RESTowymi, technicznie nimi nie są, dopiero te które spełniają wszystkie 4 poziomy są w pełni zgodne z architekturą REST a co za tym idzie możemy nazwać je RESTful.

#27
Tutaj chciałbym zaznaczyć bardzo ważną rzecz, która przez internety przewala się niemiłosiernie często, a mianowicie pytania porównujące API między sobą. Takie porównywanie API vs API generalnie nie ma sensu ponieważ te technologie mogą się na siebie nakładać / kompletować. A to które użyć, lub która jest lepsze, zależy od kontekstu i zapotrzebowania. 
Np.: stworzyć API RESTowe które pod spodem korzysta z RPC tak samo na odwrót
nie ma sensu RCP vs REST

#28
####403
Jeśli w żądaniu zostały podane dane uwierzytelniające, serwer uznaje je za niewystarczające do udzielenia
dostępu. Klient NIE POWINIEN automatycznie powtarzać żądania z tymi samymi danymi uwierzytelniającymi.
Klient MOŻE powtórzyć żądanie z nowymi lub innymi danymi uwierzytelniającymi. Jednakże, żądanie może zostać
zabronione z powodów niezwiązanych z danymi uwierzytelniającymi. Serwer źródłowy, który chce "ukryć" bieżące istnienie zabronionego zasobu docelowego MOŻE zamiast tego odpowiedzieć kodem statusu 404 Nie znaleziono

####404
Serwer źródłowy nie znalazł aktualnej reprezentacji dla zasobu docelowego lub nie chce ujawnić, że taka istnieje. Kod statusu 404 nie wskazuje, czy ten brak reprezentacji jest tymczasowy czy trwały; kod statusu 410 Gone jest preferowany zamiast 404, jeśli serwer źródłowy wie, przypuszczalnie poprzez jakieś konfigurowalne środki, że stan będzie prawdopodobnie trwały. Odpowiedź 404 jest domyślnie buforowana; tj. o ile definicja metody lub jawne kontrole buforowania nie wskazują inaczej.

#29
#### dobre praktyki
1 Serwisy REST-owe, odróżnia od serwisów SOAP-owych brak modelu kanonicznego – innymi słowy – narzuconej i wymaganej struktury danych. Z jednej strony jest to zaleta – bo daje dużą elastyczność, a z drugiej problem, bo nie możemy łatwo zdefiniować kontraktu, według którego powinny być przesyłane dane.

2 Zwracaj wartościowe odpowiedzi błędów- nie zapomnij ze API jest do komunikacji, więc się komunikuj

1. Standardowa metoda paginacji opiera się na parze: NUMER OSTATNIEGO ELEMENTU i ROZMIAR STRONY. Co jeśli między zapytaniem 3 i 4 doszedł nowy obiekt do systemu? A co jeśli jakiś obiekt został z niego usunięty? W Twoich wynikach pojawi się niespójność. Zamiast tego sortuj zawsze obiekty według stałych atrybutów – na przykład ID.

4 -

5. Gdy wprowadzasz breaking changes do swojego API lepiej stworzyć nowy endpoint niż łatać i komplikować stary. Wspieraj stare API a nowe wprowadź obok już istniejące. Z czasem możesz też monitorować użycie starego API i z chwilą zaniku jego używania dopiero je usunąć.

6 -

7. Jeśli potrzebujesz wysłać jakieś meta-dane do dostawcy API nie rozszerzaj obiektu, który wysyłasz. Zamiast tego skorzystaj z nagłówków HTTP i tam umieść informacje służące do uwierzytelnienia, włączenia specjalnych flag czy przesłania danych diagnostycznych. Treść żądań pozostaw czystym. Jak już wyżej powiedzieliśmy GET nie powinien mieć treści. W jego przypadku MUSISZ wysłać metadane w nagłówkach, więc i tak nie masz wyboru

8. Idempotentność

WOJNY KLONÓW

1. Jestem przekonany, że w każdym projekcie dojdziemy do momentu w którym pasuje nagiąć zasady REST i dodać coś co nie jest do końca zasobem a wywołaniem metody np. search. Proste filtrowanie danych możemy zrobić za pomocą istniejącego zasobu i metody GET, ale zaawansowane filtrowanie lepiej i wydajniej zrobić jako osobny endpoint search gdzie będziemy pchać dużo informacji do filtrowania za pomocą body.g