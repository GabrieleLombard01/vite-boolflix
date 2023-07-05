## Milestone 1:

Creare un layout base con una searchbar (una input e un button) in cui possiamo
scrivere completamente o parzialmente il nome di un film. Possiamo, cliccando il
bottone, cercare sull’API tutti i film che contengono ciò che ha scritto l’utente.
Vogliamo dopo la risposta dell’API visualizzare a schermo i seguenti valori per ogni
film trovato:

1. Titolo
2. Titolo Originale
3. Lingua
4. Voto

<hr>

### Milestone 1:

- **CREO** un componente STORE (in una cartella "data")
  - **COLLEGO** l'API allo STORE
- **CREO** un componente HEADER
  - con dentro INPUT e BUTTON
  - **COLLEGO** il BUTTON allo STORE
- **CREO** un componente MAIN
  - **COLLEGO** lo store al MAIN
- **QUANDO L'UTENTE** clicca sul BUTTON
  - **STAMPIAMO** a schermo le info dei film (che contengono ciò che ha scritto l’utente.)
