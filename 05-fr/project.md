# System aukcyjny

## Wprowadzenie

Specyfikacja wymagań funkcjonalnych w ramach informatyzacji procesu sprzedaży produktów w oparciu o mechanizm aukcyjny. 

## Procesy biznesowe

---
<a id="bc1"></a>
### BC1: Sprzedaż aukcyjna 

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Opis:** Proces biznesowy opisujący sprzedaż za pomocą mechanizmu aukcyjnego. |

**Scenariusz główny:**
1. [Sprzedający](#ac1) wystawia produkt na aukcję. ([UC1](#uc1))
2. [Kupujący](#ac2) oferuje kwotę za produkt wyższą od aktualnie najwyższej oferty. ([BR1](#br1)) ([UC2](#uc2))
3. [Kupujący](#ac2) wygrywa aukcję ([BR2](#br2)) ([UC2](#uc2))
4. [Kupujący](#ac2) przekazuje należność Sprzedającemu. ([UC2](#uc2))
5. [Sprzedający](#ac1) przekazuje produkt Kupującemu. ([UC2](#uc2))

**Scenariusze alternatywne:** 

2.A. Oferta Kupującego została przebita, a [Kupujący](#ac2) pragnie przebić aktualnie najwyższą ofertę.
* 2.A.1. Przejdź do kroku 2.

3.A. Czas aukcji upłynął i [Kupujący](#ac2) przegrał aukcję. ([BR2](#br2))
* 3.A.1. Koniec przypadku użycia.

---

## Aktorzy

<a id="ac1"></a>
### AC1: Sprzedający

Osoba oferująca towar na aukcji.

<a id="ac2"></a>
### AC2: Kupujący

Osoba chcąca zakupić produkt na aukcji.

<a id="ac3"></a>
### AC3: Zwyciężca

Osoba, która wygrała aukcję.


## Przypadki użycia poziomu użytkownika

### Aktorzy i ich cele

[Sprzedający](#ac1):
* [UC1](#uc1): Wystawienie produktu na aukcję
* [UC2](#uc2): Przekazanie produktu [Kupującemu](#ac1)

[Kupujący](#ac2):
* [UC2](#uc1): Licytowanie produktu

[Zwyciężca](#ac3):
* [UC2](#uc2): Wygranie aukcji
* [UC2](#uc2): Przekazanie wylicytowanej kwoty [Sprzedającemu](#ac1-sprzedający)

---
<a id="uc1"></a>
### UC1: Wystawienie produktu na aukcję

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu chęć wystawienia produktu na aukcję.
2. System prosi o podanie danych produktu i ceny wywoławczej.
3. [Sprzedający](#ac1) podaje dane produktu oraz cenę wywoławczą.
4. System weryfikuje poprawność danych.
5. System informuje o pomyślnym wystawieniu produktu na aukcję.

**Scenariusze alternatywne:** 

4.A. Podano niepoprawne lub niekompletne dane produktu.
* 4.A.1. System informuje o błędnie podanych danych.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc2"></a>
### UC2: Aukcja

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2), [Zwyciężca](#ac3)

**Scenariusz główny:**
1. [Kupujący](#ac2) składa ofertę [BR1](#br1-złożenie-oferty)
2. Po upływie czasu aukcji, system weryfikuje złożone oferty i wyznacza [Zwyciężcę](#ac3) ([BR2](#br2-rozstrzygnięcie-aukcji))
3. [Zwyciężca](#ac3) przekazuje wylicytowaną należność Sprzedającemu ([BR5](#br5-przekazanie-zapłaty-sprzedającemu))
4. [Sprzedający](#ac1) przekazuje wylicytowany produkt Kupującemu ([BR4](#br4-przekazanie-produktu-zwyciężcy))
5. Aukcja zostaje zakończona ([BR6](#br6-zakończenie-aukcji)) ([BR3](#br3-długość-trwania-aukcji))

**Scenariusze alternatywne:** 

1.A. Żaden z Kupujących nie złożył oferty, przed upływem czasu
* 1.A.1. Przejdź do kroku 5. [BR3](#br3-długość-trwania-aukcji)

3.A [Zwyciężca](#ac3-zwyciężca), nie przekazał wylicytowanej sumy Sprzedającemu
* 3.A.1 [Kupujący](#ac1-sprzedający), nie wysyła produktu Zwyciężcy
* 3.A.2 Przejdź do kroku 1.

4.A [Sprzedający](#ac1-sprzedający), nie przekazał wylicytowanego produktu [Zwyciężcy](#ac3-zwyciężca) ([BR4](#br4))
* 4.A.1 Aukcja zostaje usunięta
* 4.A.2 [Sprzedający](#ac1-sprzedający) oddaje przesłaną sumę [Zwyciężcy](#ac3-zwyciężca)

---

## Obiekty biznesowe (inaczje obiekty dziedzinowe lub informatycjne)

### BO1: Aukcja

Aukcja jest formą zawierania transakcji kupna-sprzedaży, w której Sprzedający określa cenę wywoławczą produktu, natomiast Kupujący mogą oferować własną ofertę zakupu każdorazowo proponując kwotę wyższą od aktualnie oferowanej kwoty. Aukcja kończy się po upływie określonego czasu. Jeśli złożona została co najmniej jedna oferta zakupy produkt nabywa ten Kupujący, który zaproponował najwyższą kwotę. 

### BO2: Produkt

Fizyczny lub cyfrowy obiekt, który ma zostać sprzedany w ramach aukcji.

## Reguły biznesowe

<a id="br1"></a>
### BR1: Złożenie oferty

Złożenie oferty wymaga zaproponowania kwoty wyższej niż aktualnie oferowana o minimum 1,00 PLN.


<a id="br2"></a>
### BR2: Rozstrzygnięcie aukcji

Aukcję wygrywa ten z [Kupujący](#ac2)ch, który w momencie jej zakończenia (upłynięcia czasu) złożył najwyższą ofertę.

<a id="br3"></a>
### BR3: Długość trwania aukcji

Po upłynięciu 14 dni od wystawienia produktu na aukcję, aukcja zostaje usunięta.

<a id="br4"></a>
### BR4: Przekazanie produktu Zwyciężcy

[Sprzedający](#ac1-sprzedający), ma obowiązek przekazania wylicytowanego produktu Zwyciężcy.

<a id="br5"></a>
### BR5: Przekazanie zapłaty Sprzedającemu

[Zwyciężca](#ac3), ma obowiązek przekazania wylicytowanej kwoty [Sprzedającemu](#ac1-sprzedający).

<a id="br6"></a>
### BR6: Zakończenie aukcji

Aukcja kończy się po tym jak, [Sprzedający](#ac1-sprzedający) przekaże wylicytowany produkt [Zwyciężcy](#ac3-zwyciężca).

## Macierz CRUDL


| Przypadek użycia                                  | Aukcja | Produkt | ... |
| ------------------------------------------------- | ------ | ------- | --- |
| UC1: Wystawienia produktu na aukcję               |    C   |    C    | ... |
| UC1: Podanie ceny i danych o produkcie            |  ...   |    C    | ... |
| UC2: Złożenie oferty przez kupującego             |    M   |  ...    | ... |
| UC2: Wygranie aukcji przez kupującego             |    M   |  ...    | ... |
| UC2: Zakończenie aukcji                           |    D   |  ...    | ... |

