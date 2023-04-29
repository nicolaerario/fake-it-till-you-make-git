---
layout: page
title: Come rendere la tua history git più interessante
description: Qualche convenzione su i messaggi dei commit (e sui titoli delle PR)
---

> I conventional commits sono un modo per scrivere i messaggi di commit in modo sensato.

Ci sono molti benefici ad utilizzare i `conventional commits`. Ma la prima cosa che un novizio nota è che possono semplificare il processo per _scrivere un **buon** messaggio di commit_.

Tutti gli sviluppatori sanno quanto è _difficile_ dare nomi alle cose, e scrivere nomi brevi e descrittivi è ancora più impegnativo. Fornendo un formato da seguire, i conventional commits aiutano a ridurre lo sforzo mentale richiesto per scrivere un messaggio di commit, portandoci verso la giusta direzione.

La prima cosa che devi fare prima di scrivere un messaggio di commit è chiedere a sè stessi: **_"Questo commit..."_** e completare la domanda con il tuo messaggio di commit.

Il risultato sarà qualcosa del tipo: `aggiungerà una nuova feature nel mio codice` (**attenzione**: è un esempio).

Dopo che avrai scritto un titolo di senso compiuto al tuo commit, potrai (non obbligatoriamente) scrivere un paragrafo per descrivere nel dettaglio tutto ciò che non entrerà nel limite di 50 caratteri.
Scrivi questo paragrafo **dopo una riga vuota**.

> Non hai bisogno di menzionare i file dove cambi linee di codice o altre cose che ti vengono dette da `git`; concentrati su _cosa_ fa il tuo codice.

Seguendo le convenzioni elaborate da [conventionalcommits.org](https://www.conventionalcommits.org/), ho ricavato le mie.
Il messaggio di commit dovrebbe essere strutturato come segue:

```
<tipo>[campo opzionale]: <descrizione>

[corpo del testo opzionale]

```

## Tipi

- **Fix**: un commit di tipo `fix` risolve un bug nel tuo codice.
- **Feat**: un commit di tipo `feat` introduce una nuova feature nel tuo codice.
- **Refactor**: un commit di tipo `refactor` introduce un refactor nel codice.
- **BREAKING CHANGE**: un commit al quale aggiungere `!` dopo il tipo/campo, porta alla rottura delle API. Un BREAKING CHANGE può far parte di commit di qualunque tipo.

Altri tipi oltre `Fix:`, `Feat:` e `Refactor:` sono permessi, per esempio: `Build:`, `Ci:`, `Docs:`, `Style:`, `Test:`, e altri.

Esempi:

```
fix: prevent racing of requests
feat(lang): add Italian language
refactor!: drop support for Node 6
```

## I titoli delle PR e i loro merge commit message

Quando viene creata una `release`, **GitHub** genera automaticamente il changelog usando i titoli delle `pull requests`.
Anche se si applicano le stesse regole che valgono per i commit, è preferibile rimuovere il `tipo` nella creazione del titolo. Questo renderà il changelog più leggibile.

`GitHub` utilizza dei merge commit message di default, del tipo: `Merge pull request #123 from username/branch-name`.
Naturalmente, nessuno riuscirà a capire che cosa fa questo commit leggendo questo titolo.
Per migliorare la leggibilità della cronologia del git, utilizza i titoli delle PR come merge commit message aggiungendo, alla fine, il riferimento alla `PR`.

> GitHub ha aggiunto recentemente una opzione che fa tutto questo automaticamente: _Repository > Settings > Pull Requests > Select Allow merge commits (pre selected) > Select "Default to pull request title"_

Il risultato è:

`Add conventional commits paragraph (PR #5)`

Questo renderà il log di git una _**storia** leggibile_.

## Quindi, perché usare i Conventional Commits?

- Per determinare automaticamente un bump di versione basato sulla semantica dei commit.
- Per comunicare la natura dei cambiamenti a colleghi, al pubblico o ad altri soggetti interessati.
- Per attivare i processi di build e publish.
- Per rendere più semplice ad altre persone a contribuire al tuo progetto, permettendo loro di accedere a una cronologia di commit più strutturata.
- Per generare i `CHANGELOG` automaticamente.

Questo (può) farci risparmiare molto lavoro.
