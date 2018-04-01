# Przydatne Narzedzia
Narzędzia przydatne podczas testów bezpieczeństwa

## Testy bezpieczeństwa środowiska
### SSH Audit

#### Opis
Program umożliwia wykonanie testu poprawności konfiguracji komunikacji szyfrowanej dla protokołów SSH1 i SSH2. Narzędzie rozpoznaje oprogramowanie, jego wersję, wykrywa stosowanie kompresji. 

Raport z narzędzia składa się z kilku sekcji:
- informacje ogólne – wersja oprogramowania, zwracany baner, kompresja
- algorytmy wymiany klucza
- algorytmu klucza
- algorytmy szyfrujące
- algorytmy kodu uwierzytelniania wiadomości MAC
- podsumowanie rekomendacji

W przypadku wykrycia algorytmów uznawanych za podatne lub słabe i niezalecane zwracana jest stosowana informacja wraz z informacją o podatności, czasami kodem CVE oraz informacjami historycznymi z OpenSSH, Dropbear SSH i libssh. Podsumowania zawiera pełną listę rekomendacji dotyczących poprawy bezpieczeństwa konfiguracji SSH. 
Program napisany jest w Pythonie, brak zależności, kompatybilny z Python 2.6+ i Python 3.x. Program dostępny do pobrania pod adresem https://github.com/arthepsy/ssh-audit. 

#### Przykład wywołania:
```
python ssh-audit.py 192.168.100.100
```
Ostatnio wydana wersja: v1.7.0 (2016-10-26)

#### Zastrzeżenia:
Narzędzie rekomenduje wyłączenie algorytmów ecdh-sha2-nistp521, ecdh-sha2-nistp384, ecdh-sha2-nistp256, które w innych źródłach są podawane jako bezpieczne: https://github.com/arthepsy/ssh-audit/issues/9 - algorytmy zalecane np. w wymienionych źródłach https://infosec.mozilla.org/guidelines/openssh, https://tools.ietf.org/id/draft-ietf-curdle-ssh-kex-sha2-09.html - „ecdh-sha2-nistp384 - If traditional ECDH key exchange methods are implemented, then this method SHOULD be implemented.” 

#### Rekomedacje dotyczące konfiguracji SSH:
https://tools.ietf.org/id/draft-ietf-curdle-ssh-kex-sha2-09.html

### Nmap

#### Opis

Program służący do skanowania portów i wykrywania usług w sieci. Program implementuje wiele różnych technik testowania portów TCP, UDP oraz SCTP w tym niestandardowe podejścia wynikające ze specyfiki implementacji stosów sieciowych, które potencjalnie mogą omijać zapory sieciowe lub platformy Intrusion Detection System. Dodatkowo Nmap posiada możliwość identyfikacji systemów operacyjnych na skanowanych hostach.

Możliwości programu:
- Identyfikacja hostów - wykrycie, pod jakimi adresami IP w danej sieci znajdują się działające hosty
- Skanowanie portów - wylistowanie otwartych portów
- Detekcja wersji - wykrycie nazw i wersji aplikacji
- Detekcja systemu operacyjnego - wykrycie systemu operacyjnego, czy charakterystyki sprzętowej
- Możliwość użycia we własnych skryptach
- Jest to najpopularniejsze narzędzie, w porównaniu do innych, dość efektywne w jednoczesnym przeprowadzaniu skanowania wielu portów/ hostów. Narzędzie jest darmowe udostępniane na licencji open source.

#### Hearbleed

Weryfikacja występowania błędu Heartbleed (błąd bezpieczeństwa w popularnej bibliotece kryptograficznej OpenSSL, zaliczany do grupy błędów implementacyjnych, pozwalający na odczyt przez atakującego danych, chronionych przez szyfrowanie SSL i TLS, wyciek losowych 64 Kb danych, także identyfikatorów sesji, kluczy prywatnych itp.). Podatne są wersje OpenSSL z serii 1.0.1 oraz 1.0.2-beta. Błąd z roku 2014 - CVE-2014-0160.

```
nmap -d --script ssl-heartbleed --script-args vulns.showall -sV <host>
nmap -p 443 --script ssl-heartbleed <host>
```
