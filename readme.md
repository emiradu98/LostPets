# Lost Pets Architecture

Proiect la materia Retele de Calculatoare ce consta intr-un server web implementat prin socketi ce rezolva cerintele clientilor in mod concurent.

## Enunt proiect

Creați o aplicație Web care să vină în ajutorul recuperării animalelor pierdute de o persoana. Proprietarul animalului pierdut va completa un formular cu detalii despre acesta: nume, fotografie, zona în care a fost ultima dată văzut, plus alte detalii de interes (specie, existenta unor semnalmente, date despre zgarda, medalion, recompense acordate,...) si modalități de contact (minimal, adresa e-mail + numar de telefon). Odată adăugate aceste date, toți utilizatorii aflați în acea zonă vor fi automat notificați. Locul ultimei vizualizări a animalului poate fi actualizat de ceilalți utilizatori, schimbându-se astfel zona și fiind deci notificați alți oameni.

Anunțurile vor fi afisate în ordine cronologica, fiind figurate pe baza unor servicii cartografice OpenStreetMap. Se vor genera statistici de interes -- disponibile in formatele HTML, CSV si PDF -- privind cazurile de animale pierdute, recuperarea acestora, zonele cele mai vulnerabile, recompense etc.

### Use cases

1. Userul introduce datele in formularul de login, este redirectionat pe pagina principala, de unde selecteaza un animal pe care l-a vazut. Face un update la pagina animalului.

2. Adminul site-ului acceseaza pagina de login administrativ, ii apare pagina de monitorizare a aplicatiei web de unde genereaza statistici in format pdf a numarului de animale pierdute si recuperate in Nicolina.

3. Userul acceseaza pagina de profil pentru a modifica detalii precum poza de profil, adresa de email si pentru a vizualiza animalele pe care le-a gasit sau pe care le-a pierdut.

4. Userul acceseaza sectiunea de notificari, apasa pe “[Pet name] has been found thanks to your contribution!”. De aici user-ul este redirectionat catre pagina animalului pe care l-a gasit pentru a-si lua recompensa in cazul in care exista.

5. Userul acceseaza pagina de introducere a unui animal pe care l-a pierdut. Dupa ce introduce toate informatiile necesare este redirectionat pe o pagina noua creata pentru animalul introdus. Cativa alti useri updateaza locatia animalului, iar un altul il gaseste.

6. Userul acceseaza site-ul pentru prima oara. Doreste sa isi creeze cont, apasa pe "Sign up" si este redirectionat pe pagina cu formularul de inregistrare. Userul completeaza toate datele necesare, iar la apasarea butonului "Register" un mail de confirmare al contului este trimis pe adresa utilizatorului. Acesta este rugat sa confirme contul inainte de a putea accesa continutul site-ului.

### APIs

1. Firebase API

```
$gcc simpleWeb.c -o simpleWeb.bin
```

2. OpenStreetMaps API

```
$./simpleWeb.bin
```

### Autentificare persistenta

Se va realiza prin folosirea tool-ului Firebase Authentification.

1. Inregistrarea se va face prin intermediul metodei 
```
.createUserWithEmailAndPassword(email,password)
```
2. Dupa inregistrare utilizatorul este logat automat.
3. Salvarea sesiunii si modificarilor din cadrul sesiunii se va face folosind metoda 
```
.onAuthStateChanged(firebaseUser => {})
```
4. Logarea in cazul delogarii se va face folosind metoda
```
.signInWithEmailAndPassword(email,password)
```

## Realizat cu

* [VSC](https://code.visualstudio.com) - IDE-ul utilizat
* [C](http://www.cplusplus.com) - limbajul de programare
* [HTTP 1.1 Protocol](https://www.w3.org/Protocols/rfc2616/rfc2616.html) - protocolul de transfer

## Autor

* **Radu Emilian** - *Simple Web Server*



Inainte de a compila trebuie facute configurari in fisierul config.txt. 
Cel mai important aspect este modificarea adresei serverului (unde o sa se afle fisierele ce vor fi accesate de browser).
In fisierul config.txt modificati linia 2:

```
Locatie: /Users/Emilian/Documents/site 
```
Dupa textul "Locatie: " introduceti adresa absoluta de pe sistemul dumneavoastra ca in exemplul de mai sus.
Este foarte important ca la finalul adresei sa fie un spatiu!
Programul nu va rula daca adresa nu este cea de pe sistemul pe care va rula serverul / daca nu este un spatiu la finalul liniei.

Urmatoarea linie ce poate fi modificata este:
```
Port: 8001
```

Unde portul poate fi orice alta valoare. Poate fi lasat nemodificat, insa trebuie specificat in adresa din browser pentru a se putea accesa sub forma :
```
localhost:8001 | localhost:<Port>
```

Alte modificari:
```
Index index.html 
```
(un spatiu la sfarsitul liniei) daca se doreste ca pagina default pe care o furninzeaza serverul sa fie alta.
Se va modifica "index.html" cu orice alt fisier cu extensia .txt sau .html