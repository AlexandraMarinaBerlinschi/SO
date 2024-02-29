# SO - Sisteme de Operare
## Web Server 

Problema se încadrează în domeniul rețelelor de calculatoare și programării concurente.
Principalele provocări includ gestionarea concurenței, sincronizarea proceselor și alocarea eficientă a resurselor pentru a procesa cererile HTTP în mod eficient.
Proiectul implică implementarea unui server web concurent capabil să gestioneze multiple cereri HTTP simultan, inclusiv GET, HEAD, POST și PUT.
Datele Particulare ale Problemei:
- Gestionarea cererilor HTTP multiple într-un mod eficient și sigur.
- Implementarea corectă a diferitelor metode HTTP (GET, HEAD, POST, PUT).
- Concurența și procesarea paralelă folosind fork().
  
Scopul este de a dezvolta un server web stabil și eficient care să poată servi conținut static și să proceseze cereri într-un mod concurent.

Ținta Proiectului: Oferirea unei soluții eficiente pentru site-uri mici și medii, cu posibilitatea de extindere pentru nevoi suplimentare.
Use-Case-uri Minimale:
- Servirea conținutului web static, cum ar fi pagini HTML, imagini și fișiere CSS/JS.
- Handling GET request for: /4k.jpeg Bytes Sent: 1188839, Time Taken: 0.018039 seconds, Throughput: 65903819.502190 bytes/sec
- Procesarea cererilor dinamice, inclusiv primirea și trimiterea de date JSON.
- Handling GET request for: /Json.json Bytes Sent: 226, Time Taken: 0.000169 seconds, Throughput: 1337278.106509 bytes/sec
  
Cerințe de Sistem și Mediu de Dezvoltare
- Sistem de Operare: Linux sau alte sisteme Unix-like.
- Biblioteci Software: Utilizează biblioteci standard C și biblioteca Jansson pentru manipularea JSON.
  
Specificatii tehnice și de integrare:
- Serverul este implementat în C și este compatibil cu sistemele de operare bazate pe Unix.
- Suportă interacțiunea cu alte sisteme prin intermediul protocolului HTTP

  Serverul web este construit pe o arhitectură bazată pe procese, utilizând modelul client-server. Mecanisme și Algoritmi Folosiți:
- Forking Model: Pentru gestionarea concurenței, serverul folosește modelul de forking, creând un nou proces pentru fiecare cerere HTTP primită.
- Procesarea HTTP: Implementarea metodelor HTTP (GET, POST, etc.) prin interpretarea și răspunderea corespunzătoare la cererile clientului.
  
Alegerea Mecanismelor și Algoritmilor:
- Alegerea modelului de forking este motivată de simplitatea sa și de capacitatea de a izola fiecare cerere, evitând interferențele între procese.
- Metodele HTTP sunt implementate pentru a asigura conformitatea cu standardele web și pentru a oferi funcționalități de bază ale unui server web.
  
Diferențe față de Alte Abordări:
- Față de serverele thread-based sau event-driven, acest server prioritizează izolarea și siguranța proceselor, acceptând un consum mai mare de resurse.
- Abordarea se concentrează pe simplitate, ideală pentru aplicații de dimensiuni mici și medii.

Biblioteci Software Folosite:
1. Biblioteci Standard (stdlib.h, string.h, stdio.h): Utilizate pentru manipularea stringurilor, alocare de memorie, și operații I/O.
2. Sockets API (sys/socket.h, arpa/inet.h, unistd.h): Esențiale pentru funcționalități de rețea precum crearea și gestionarea socket-urilor.
3. Jansson (jansson.h): Folosită pentru manipularea datelor JSON, utilă în cererile și răspunsurile HTTP.

Probleme Tehnice și Soluții:
1. Concurența: Inițial, utilizarea `fork` pentru fiecare cerere nouă limita performanța. Pentru a rezolva problema concurenței, am explorat utilizarea thread-urilor în locul proceselor copil.
2. Parsing-ul Cererilor HTTP: Probleme în extragerea corectă a componentelor cererilor. Soluția a fost îmbunătățirea algoritmului de parsing.

Limitările Implementării
1. Scalabilitate: Actuala implementare, bazată pe procese copil (`fork`), nu este cea mai scalabilă soluție pentru un webserver. În condiții de trafic ridicat, aceasta poate deveni o limitare majoră, și chiar devine la partea de implementare.
2. Securitate: Nu am implementat măsuri avansate de securitate, ceea ce ar putea face serverul vulnerabil la diverse atacuri, cum ar fi injection sau DoS.
3. Flexibilitate în Rutare și Middleware: Serverul nostru este relativ simplist în gestionarea rutei și
nu suportă middleware complex sau rutare avansată, ceea ce limitează capacitatea sa de a servi
aplicații web complexe, de asemenea nu dispune de procesarea cererilor dinamice cum ar fi
scripturi PHP.
4. Performanța în Tratarea Fișierelor Statice: Manipularea fișierelor statice, cum ar fi HTML, CSS,
și imagini, nu este optimizată. În implementarea curentă, fiecare cerere de fișier static este tratată
individual, ceea ce poate duce la întârzieri în încărcarea conținutului.
