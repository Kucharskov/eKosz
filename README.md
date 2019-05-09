# eKosz (repozytorium archiwalne)
System inteligentnego kubła na śmieci zrealizowany w C++ na wbudowanej pamięci mikrokontrolera ESP8266 oraz w formie aplikacji desktopowej napisanej w języku C#.

## Autorzy
Projekt został wykonany przez studentów Politechniki Śląskiej na wydziale Wydział Inżynierii Materiałowej i Metalurgii na kierunku Informatyka Przemysłowa:
* Michał Kucharski (https://kucharskov.pl)
* Michał Lewicki (https://michalewicki.github.io)
* Sebastian Marzec

## Założenia
Część pierwsza dotycząca przedmiotu "Zaawansowane programowanie w języku C":
* realizacja i umieszczenie wszystkich danych jedynie na pamięci mikrokontrolera,
* realizacja kodu w sposób naprzemienny(przeplot) pomimo jednego wątku układu,
* łatwość modyfikacji ustawień w kodzie,
* prostota dodawania kolejnych elementów,
* prostota i łatwość użycia przez zewnętrznego użytkownika.

Część druga dotycząca przedmiotu "Aplikacje wielowarstwowe":
* odtworzenie funkcjonalności oferowanej przez układ w formie aplikacji desktopowej,
* weryfikacja połączenia z urządzeniem,
* nieblokujący interfejs działający w sposób asynchroniczny,
* prostota interfejsu i użytkowania aplikacji,
* odporność aplikacji na niepoprawne użytkowanie.

## Rezalizacja części pierwszej
Do realizacji projektu z części programowania w języku C użyto modułu ESP8266 oraz zestaw elementów:
* DHT11 – czujnik temperatury i wilgotności,
* MPU6050 – 3-osiowy akcelerometr i żyroskop z wbudowanym termometrem,
* BMP280 – cyfrowy barometr,
* TSL2561 – czujnik natężenia światła otoczenia,
* HC-SR04 – ultradźwiękowy czujnik odległości,
* S90 – serwomechanizm modelarski.

![Cały układ](https://github.com/Kucharskov/eKosz/blob/master/images/circuit.jpg?raw=true)
![Układ zamontowany w obudowie](https://github.com/Kucharskov/eKosz/blob/master/images/circuit_mount.jpg?raw=true)

Urządzenie po podłączeniu zasilania uruchamia Hotspot „eKosz” na czas określony z góry (300s) w celu konfiguracji urządzenia. W przypadku braku konfiguracji urządzenie przechodzi w tryb uśpienia, wyłączając hotspot oraz usypiając wszystkie czujniki.Natomiast po konfiguracji, którą jest podłączenie urządzenia do zadanej sieci WiFi zaprojektowane oprogramowanie pozwala na:
* sprawdzenie stanu urządzenia(pozycja klapy, ilość otwarć, poziom wypełnienia),
* otwarcie i zamknięcie klapy „eKosza”,
* wyświetlanie bieżących danych dostępnych czujników,

![Menu konfiguracji WiFi](https://github.com/Kucharskov/eKosz/blob/master/images/wifi_config.jpg?raw=true)
![Serwowana strona WWW](https://github.com/Kucharskov/eKosz/blob/master/images/webpage.jpg?raw=true)

Dane aktualizowane są co zadany czas (60s) z informacją o przedawnieniu lub braku danych. Powyższe możliwości zrealizowane są za pomocą wbudowanego serwera WWW, serwującego stronę, która odpytuje urządzenie o potrzebne dane za pomocą asynchronicznych zapytań GET i POST w języku JavaScript. Dane przesyłane są w formacie JSON.

## Rezalizacja części drugiej
Do realizacji projektu z części aplikacje wielowarstwowe użyto języka C# w celu napisania aplikacji desktopowej. Pierwotnie jedyną opcją jest wprowadzenie adresu do połączenia z urządzeniem. Podczas próby połączenia następuje:
- weryfikacja adresu pod względem składni adresu URL,
- normalizacja adresu – ciąg musi rozpoczynać się od „http://” i kończyć na „/”,
- weryfikacja czy pod danym adresem znajduje się API zaprojektowanego urządzenia w części pierwszej.

gdzie w razie napotkanych wyjątków zgłaszane są do użytkownika stosowne komunikaty np.: „Podany adres jest nieprawidłowy!”, „Podany adres jest niedostępny lub nie jest adresem eKosza!”. W przypadku braku wyjątków odblokowywana jest reszta interfejsu, która pozwala na:
- otworzenie i zamknięcie klapy urządzenia,
- pobranie danych na temat stanu urządzenia i jego czujników,
- rozłączenie w celu nawiązania połączenia z innym urządzeniem.

![Działająca aplikacja](https://github.com/Kucharskov/eKosz/blob/master/images/ekoszapp.jpg?raw=true)

## Ostateczny efekt
![Całe urządzenie](https://github.com/Kucharskov/eKosz/blob/master/images/ekosz.jpg?raw=true)

> **Notka:** Repozytorium w celach archiwalnych, nie zanosi się na wprowadzanie poprawek :)