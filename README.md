# CryptoMining 1.0.0 — Paper 1.21.11

Wirtualne kopanie BTC, ETH i DOGE za pomocą koparek. To **nie** jest prawdziwy miner kryptowalut.

## Wymagania
- Serwer **Paper 1.21.11**, **Java 21**
- **Vault** i plugin dostarczający ekonomię Vault, np. **EssentialsX** z aktywną ekonomią
- Do zbudowania: **Maven 3.9+** oraz JDK 21

## Budowanie
1. Otwórz terminal w folderze zawierającym `pom.xml`.
2. Wykonaj `mvn clean package` (wymagany internet do pobrania zależności).
3. Gotowy plik znajdziesz w `target/CryptoMining-1.0.0.jar`.

## Instalacja
1. Wyłącz serwer.
2. Skopiuj `CryptoMining-1.0.0.jar` do `plugins/`.
3. Upewnij się, że masz Vault i EssentialsX (z ekonomią).
4. Uruchom serwer i wpisz `/crypto`.
5. Zmień `plugins/CryptoMining/config.yml` i wpisz `/crypto reload`.

## Komendy
- `/crypto` — GUI główne
- `/crypto sklep` — kupowanie koparek
- `/crypto portfel` — portfel; kliknięcie sprzedaje całe saldo danej waluty
- `/crypto gielda` — bieżące ceny
- `/crypto koparki` — posiadane koparki
- `/crypto kup BTC BASIC` — kup koparkę BASIC dla BTC
- `/crypto sprzedaj BTC 0.1` lub `/crypto sprzedaj BTC all` — sprzedaj kryptowalutę
- `/crypto give <gracz-online> <BTC|ETH|DOGE> <ilosc>` — admin
- `/crypto reload` — admin

Uprawnienie administratora: `cryptomining.admin` (domyślnie OP).

## Mechanika
- Każda koparka przypisana jest do jednej waluty.
- Co `mining-interval-seconds` sekund (domyślnie 60) nalicza określoną liczbę monet, również dla graczy offline, o ile serwer jest uruchomiony.
- Co `market-update-seconds` sekund kurs zmienia się losowo w granicach ustalonych w konfiguracji.
- Koparki są wirtualne: nie trzeba ich stawiać w świecie. Brak kosztów prądu.
- Dane i kursy są przechowywane w `plugins/CryptoMining/players.yml`.

## Uwagi
- To projekt źródłowy. W tej paczce **nie ma skompilowanego JAR**, ponieważ środowisko przygotowania nie ma dostępu do repozytoriów Maven.
- Projekt nie był kompilowany ani testowany na uruchomionym serwerze. Zalecany test na serwerze stagingowym.
- W razie zmiany wersji Paper sprawdź dostępność odpowiedniej wersji `paper-api` w `pom.xml`.
- Przy operacjach Vault i zapisie YAML nie ma pełnej transakcyjności w przypadku nagłej awarii serwera. Warto regularnie robić kopie danych.
