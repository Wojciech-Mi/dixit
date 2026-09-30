# ✦ Dixit Companion – Licznik Punktów i Głosowanie

Lekka aplikacja webowa wspierająca rozgrywkę w grę planszową **Dixit** (do 12 graczy). Zastępuje fizyczne żetony do głosowania oraz tor punktacji – każdy gracz głosuje i oznacza swoją kartę bezpośrednio na ekranie własnego telefonu.

## ✨ Główne funkcje

* **Błyskawiczne dołączanie (QR / Kod Stołu):** Gracze dołączają do stołu przez przeglądarkę w telefonie po zeskanowaniu kodu QR z ekranu Hosta – bez instalowania aplikacji i zakładania kont.
* **Działanie bez serwera (WebRTC P2P):** Dzięki bibliotece PeerJS telefony łączą się bezpośrednio z urządzeniem Hosta. Aplikacja działa od razu po wrzuceniu samego pliku `index.html` na darmowy hosting statyczny (np. GitHub Pages).
* **Pamięć sesji (`localStorage`):** Przypadkowe odświeżenie strony lub zamknięcie przeglądarki nie kasuje punktów ani miejsca gracza przy stole.
* **Animowane odsłanianie kart 3D:** Budujące napięcie odkrywanie kart po każdej rundzie – od kart bez głosów, przez karty ze zmyłkami, aż po finałową kartę Bajarza.
* **Wsparcie dla osób słabowidzących:**
  * **👁️ Duży UI:** Tryb wysokiego kontrastu (czarno-żółty) z powiększonymi kafelkami kart.
  * **🔍 Lupa Stołowa:** Podgląd z tylnego aparatu telefonu z płynnym przybliżeniem (`1.0x – 5.0x`), przesuwaniem palcem oraz funkcją **„Zatrzymaj kadr”** (zamraża obraz w pamięci bez zapisywania zdjęć w telefonie).
* **Panel Hosta (⚙️):** Ustalanie kolejności Bajarzy i kolorów w Lobby, pauzowanie nieobecnych graczy (status AFK), ręczna korekta punktów, wymuszanie kolejnego kroku, tryb szybkiego odkrywania kart (`1.3s` zamiast `2s`) oraz opcjonalne automatyczne przechodzenie do następnej rundy (`15s`).

## 🎲 Przebieg rundy i punktacja

1. **Ruch Bajarza:** Bajarz podaje skojarzenie, zbiera karty od graczy, tasuje je i rozkłada na stole od `1` do `N`, po czym zatwierdza gotowość w aplikacji.
2. **Tajne głosowanie:** Wszyscy gracze (poza Bajarzem) wybierają na telefonach numer karty, która ich zdaniem należy do Bajarza.
3. **Oznaczanie własnej karty:** Po zakończeniu głosowania każdy gracz (w tym Bajarz) wskazuje numer swojej karty. W przypadku kliknięcia tej samej karty przez dwie osoby aplikacja wyświetla ostrzeżenie o konflikcie i pozwala poprawić wybór.
4. **Podliczenie punktów:**
   * **Trafienie karty Bajarza:** `+3 pkt` dla Bajarza oraz każdego gracza, który odgadł kartę.
   * **Nikt nie zgadł lub wszyscy zgadli:** Bajarz otrzymuje `0 pkt`, a pozostali gracze po `+2 pkt`.
   * **Zmyłki:** `+1 pkt` za każdy głos oddany przez innych graczy na Twoją kartę (naliczane zawsze, bez limitu). Głos oddany na własną kartę daje `0 pkt`.

## 🚀 Uruchomienie

### Wariant 1: GitHub Pages (Zalecany)
1. Wgraj plik `index.html` do repozytorium na GitHubie.
2. Wejdź w **Settings → Pages** i w sekcji **Build and deployment** wybierz gałąź `main`.
3. Otwórz wygenerowany link `https://...` na telefonie (połączenie HTTPS jest wymagane do działania aparatu w funkcji Lupy) i kliknij **Załóż Stół (Host)**.

### Wariant 2: Lokalny serwer Node.js (Opcjonalnie)
W aplikacji (na ekranie startowym) możesz pobrać gotowy plik `server.js` i uruchomić go lokalnie w jednym folderze z `index.html`:

```bash
npm init -y && npm install express socket.io
node server.js
