# Zadanie 1

![alt text](image-29.png)

---

# Zadanie 2

![alt text](image-30.png)

### A

#TODO

### B

**Lemat:**
Jeżeli pośród $n=2k$ elementów jest $k+x$ elementów rodzaju $e$, to par elementów $e$ jest nie mniej niż o $x$ więcej niż wszystkich innych par.
**d-d:**
Jeżeli chcemy utworzyć minimalnie-wiele par elementu $e$, to rozłożymy $k$ elementów do $k$ *różnych* par oraz pozostałymi $x$ utworzymy $x$ par.
Teraz by utworzyć parę *innego* elementu potrzebujemy przełożyć $k$ gdzieś indziej – utworzyć dodatkową parę, więc tworząc parę *innego elementu* tworzymy dodatkowo parę elementu typu $e$ – tych par jest o $x$ więcej od par pozostałych elementów.

To również dowodzi przypadku dla $n = 2k+1$, bo jeżeli *ostatni* element jest elementem większościowym, to mamy $k$ większościowych elementów oraz $k$ innych – par będzie co najwyżej równa ilość, ale dodatkowy większościowy przeważy.
Jeżeli *ostatni* nie jest większościowy, to mamy co najmniej $k+2$ większościowych na $k$ par – będą o dwie pary większościowe większe – wszystko działa.

#### Algorytm

Połącz sąsiednie elementy w pary $\{(0,1), (2,3), \dots\}$, następnie do następnej iteracji przenieś po jednym elemencie z par takich samych elementów.
Jeżeli elementów było nieparzyście-wiele, to po przejściu wszystkich par porównaj ostatni element ze wszystkimi innymi. Jeżeli występuje on $k$ razy dla $n = 2k+1$ to dodaj ten element do zbioru.

Jeżeli na koniec otrzymamy jeden element, to jest to *kandydat* na element większościowy.
By to sprawdzić liczymy jego wystąpienia w tablicy i jeżeli jest ich faktycznie więcej to wracamy.

#### Dowód Poprawności

**Niezmiennik:**

- Jeżeli istnieje element większościowy, to jest on elementem większościowym podzbioru $P$.

**Inicjalizacja:**
Na początku $P = A$, więc oczywiście mamy zależność.

**Krok Algorytmu:**
Załóżmy, że istnieje element większościowy $e\in A$. Pokażmy, że jeżeli przed iteracją $e$ jest elementem większościowym $P$, to po iteracji jest elementem większościowym $P'$.
Niech $n$ wyznacza liczność $P$.

Jeżeli $2\mid n$, to mamy $n = 2k$ oraz wiemy, że elementów $e$ jest $k + x$ dla $x > 0$. Z lematu wiemy, że par elementów $e$ będzie więcej niż pozostałych par o co najmniej $x$.

Jeżeli $2 \nmid n$, to mamy $n = 2k + 1$ oraz wiemy, że elementów e jest $k + x$ dla $x > 0$. Teraz jeżeli ostatni element to $e$, to par $e$ z pierwszych $2k$ elementów może być tyle samo co innych, ale dołożymy ostatni element po sprawdzeniu, że w pierwszej części jest ich co najmniej $k$.
Jeżeli jakiś inny element jest ostatni, to argument jak dla $2\mid n$ i nie dokładamy dodatkowego ostatniego elementu (większość jest $e$).

---

# Zadanie 3

![alt text](image-31.png)

złożoność dzielenia (łączna) $rlogn$, bo każdy przedział $(p, k)\in S$ pojawia się w maksymalnie $logn$ przedziałach

złożoność czasowa całego 
$T(n)=2T(\frac{n}{2}) + \theta(n)$

---

# Zadanie 4

![alt text](image-32.png)

**Algorytm**
```
posortuj proste po współczynniku kierunkowym a, pozbywamy się równoległych
stack = [] 
for l in proste:
	if len(stack) == 0:
		stack.push((l, None))
	if len(stack) == 1:
		# cross oblicza punkt przecięcia dwóch prostych
		stack.push((l, cross(l, stack.top())))
	for l in proste:
		(k, x) = stack.top()
		# usuwamy proste ze stosu, które są przesłaniane przez l
		while k(x) < l(x): 
			stack.pop()
			(k, x) = stack.top()
		stack.push(l, cross(l, k))
```
Złożoność tego algorytmu (bez sortowania) to $O(n)$ czasowa (bo każdy element może być "rozważany" tylko dwa razy, raz przy dodawaniu na stos i raz przy usuwaniu)
Pamięciowa $O(n)$

ostatecznie czasowa to $O(nlogn)$ 

**Lemat**
mamy stos z prostymi stworzony przez algorytm i prostą l.
niech k to prosta z góry stosu, $x_0$ to punkt przecięcia k z drugą z góry prostą ze stosu.
jeśli l(x) > k(x) to l przesłania prostą k. 
(fakt, że są posortowane po 'a' pomaga)

Jak mamy ten lemat to w widać, że usuwamy tylko przesłonięte proste.
Jakiś dowód z niezmiennikiem, że w każdym kroku pętli mamy na stosie tylko widoczne proste z tych rozważanych do tej pory.

---
# Zadanie 5

![alt text](image-33.png)

## k = 2

$x = a \cdot 2^m + b$, gdzie $a$ i $b$ to połowy liczby $x$
$$x^2=(a\cdot 2^m+b)^2=a^2\cdot2^{2m}+2ab\cdot2^m+b^2$$
$2ab = (a + b)^2 - a^2 - b^2$

Czyli musimy rekurencyjnie obliczyć:
- $a^2$
- $b^2$
- $(a+b)^2$

$T(n)=3T(\frac{n}{2}) + n$
$T(n)=\Theta(n^{log_{2}3})$, czyli otrzymaliśmy taką samą złożoność jak algorytm karatsuby dla $k=2$

## k = 3

$x= a \cdot 2^{2m} + b \cdot 2^m + c$
$$x^2 = a^2\cdot2^{4m} + 2ab\cdot2^{3m}+(b^2+2ac)\cdot2^{2m} + 2bc\cdot2^m+c^2$$

## nie da się asymptotycznie szybciej kwadracić niż mnożyć

$(a+b)^2 = a^2 + 2ab + b^2$

$a\cdot b = \frac{(a+b)^2 - a^2 - b^2}{2}$ 

możemy mnożyć kwadracić, więc gdybyśmy mogli szybciej kwadracić to moglibyśmy szybciej mnożyć.


---

# Zadanie 6

![alt text](image-34.png)

---
# Zadanie 7

![alt text](image-35.png)

Rozwiązuję zadanie b.

- $e[\:]$ - lista sąsiedztwa drzewa
- $size[\:]$ - tablica z wielkościami poddrzew zakorzenionych w danym wierzchołku

```
fun get_size(v, p=-1):
	size[v] = 1
	for i in e[v]:
		if i == p: continue
		size[v] += get_size(i, v)
	return size[v]
```

```
fun get_centroid(v, p=-1):
	for i in e[v]:
		if i == p: continue
		if size[i] * 2 > n:
			return get_centroid(i, v)
	return v
```

Korzystamy z tych dwóch funkcji w taki sposób:
```
get_size(0)
centroid = get_centroid(0)
to_check[centroid] = true # nasza granica dla poddrzewa
```

**Lemat**
Funkcja get_size i get_centroid zwraca centroid w drzewie w $O(n)$, niezależnie od tego gdzie zaczniemy.

Następnie wywołujemy się rekurencyjnie dla każdego centroidu:
1) tab[]
2) puszczamy dfs-a szukającego odległość wierzchołków od centroidu
3) count()

```
def count(centroid):
	for i in e[centroid]:
		find_paths(i, centroid)
		add_subtree(i, centroid)
	zero_tab()
```

find_paths() zlicza ile jest ścieżek pomiędzy poddrzewami centroidu oddalonymi o C

add_subtree() uzupełnia tab o wierzchołki z poddrzewa i

---

# Zadanie 8

![alt text](image-36.png)

Podczas scalania:
```python
def merge_and_count(L, R):
    merged = []
    i = j = 0
    while i < len(L) and j < len(R):
        if L[i] <= R[j]:
            merged.append(L[i])
            i += 1
        else:
            merged.append(R[j])
            count += len(L) - i
            j += 1
    # dodajemy to co zostało
    merged.extend(L[i:])
    merged.extend(R[j:])
    return merged
```

to zwróci dokładnie tyle inwersji ile jest, dowód indukcyjny.
W kroku indukcyjnym zauważamy, że jeśli $x \in R$ jest mniejsze od $y \in L$ to $x$ jest w inwersji ze wszystkimi pozostałymi elementami $L$, od $y$ do końca.
Nasz algorytm poprawnie je zliczy.

---

# Zadanie 9

![alt text](image-37.png)

#TODO 

> Wzorcowe ma głębokość $O(n \log \log n)$

---

# Zadanie 10

![alt text](image-38.png)