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
>python ssh-audit.py 192.168.100.100
```
Ostatnio wydana wersja: v1.7.0 (2016-10-26)

#### Zastrzeżenia:
Narzędzie rekomenduje wyłączenie algorytmów ecdh-sha2-nistp521, ecdh-sha2-nistp384, ecdh-sha2-nistp256, które w innych źródłach są podawane jako bezpieczne: https://github.com/arthepsy/ssh-audit/issues/9 - algorytmy zalecane np. w wymienionych źródłach https://infosec.mozilla.org/guidelines/openssh, https://tools.ietf.org/id/draft-ietf-curdle-ssh-kex-sha2-09.html - „ecdh-sha2-nistp384 - If traditional ECDH key exchange methods are implemented, then this method SHOULD be implemented.” 

#### Rekomedacje dotyczące konfiguracji SSH:
https://tools.ietf.org/id/draft-ietf-curdle-ssh-kex-sha2-09.html

