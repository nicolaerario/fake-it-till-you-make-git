---
layout: page
title: Come rendere la tua history meno noiosa
description: Come scrivere utili messaggi di commit (ed i titoli delle PR)
---

> Seguire i conventional commits è un modo per scrivere i messaggi di commit significativi.

Ci sono molti benefici ad utilizzare i `conventional commits`, ma quello da subito più evidente è che possono semplificare il processo per _scrivere un **buon** messaggio di commit_.

Tutti gli sviluppatori sanno quanto è _difficile_ dare nomi alle cose (_qualcuno ha detto variabili?_), e scrivere nomi brevi e descrittivi è ancora più impegnativo. Fornendo uno standard da seguire, i conventional commits aiutano a ridurre lo sforzo richiesto per scrivere un buon messaggio di commit, indicandoci la giusta direzione.

La prima cosa che bisogna fare prima di scrivere un messaggio di commit è chiedersi: **_"This commit will..."_**  
e completare la domanda con il tuo messaggio di commit.

Il risultato sarà qualcosa del tipo: `... Add a new feature in my code` (**attenzione**: è un esempio, davvero!..).

Dopo aver scritto quindi un titolo di senso compiuto al commit, si potrà (non obbligatoriamente) scrivere un paragrafo per descrivere nel dettaglio tutto ciò che non entra nel limite di 50 caratteri (limite di lunghezza convenzionale per un titolo di commit).
Questo paragrafo, detto `body` del commit, va messo **dopo essere andati a capo ed inserito una riga vuota**.

> Non c'è bisogno di menzionare, nel titolo o nel body, i file dove cambi linee di codice o altri dettagli che ti vengono _già detti_ da `git` (nel `diff`); concentrati su _cosa_ fa il tuo codice.

Seguendo le idee propste da [conventionalcommits.org](https://www.conventionalcommits.org/), ho derivato le mie personali convenzioni.

Il messaggio di commit dovrebbe essere strutturato come segue:

```
<tipo>[campo opzionale]: <descrizione>

[corpo del testo opzionale]

```

## Tipi

- **Fix**: un commit di tipo `fix` risolve un bug nel codice.
- **Feat**: un commit di tipo `feat` introduce una nuova funzionalità nel codice.
- **Refactor**: un commit di tipo `refactor` introduce un refactor nel codice.
- **BREAKING CHANGE**: Se il codice presente nel commit porta una BREAKING CHANGE, si aggiunge `!` dopo il tipo/campo in modo da saltare subito all'occhio.

Altri tipi oltre `Fix:`, `Feat:` e `Refactor:` sono permessi, per esempio: `Build:`, `Ci:`, `Docs:`, `Style:`, `Test:`, ecc.

Esempi:

```
fix: Prevent racing of requests
feat(lang): Add Italian language
refactor!: Drop support for Node 6
```

## I titoli delle PR e dei relkativi merge commits

Quando viene creata una `release` ([guarda: Release the power of your code! - Make a Release](/docs/en/release-flow.md)), **GitHub** ne genera automaticamente il changelog usando i titoli delle `pull requests`.
Anche se si possono applicare le stesse regole che valgono per i commit, è preferibile omettere il `tipo` per il titolo di una PR. Questo renderà il changelog più leggibile anche ai _non addetti ai lavori_.

`GitHub` utilizza dei messaggi di default per i `merge commit` delle PR, del tipo: `Merge pull request #123 from username/branch-name`.
Un titolo del genere è però poco informativo, ma possiamo editarlo e migliorarlo.
Per migliorare la leggibilità della history, utilizza lo stesso titolo della PR come come messaggio di merge commit aggiungendo, alla fine, il riferimento alla PR stessa tra parentesi.

> GitHub ha aggiunto recentemente un' opzione che fa tutto questo automaticamente: _Repository > Settings > Pull Requests > Select Allow merge commits (pre selected) > Select "Default to pull request title"_

Il risultato sarà:

`Add conventional commits paragraph (PR #5)`

Questo renderà la history del progetto come l'indice di un libro, con i merge commit delle PR come _capitoli_ ed i commit come _paragrafi_

## Quindi, perché usare i Conventional Commits?

- Per determinare automaticamente un `bump` di versione basato sulla semantica dei commit. ([guarda: Versioning](/docs/en/release-flow.md#versioning))
- Per comunicare in modo immediato la natura dei cambiamenti nel codice a colleghi, ai non addetti ai lavori o ad altri soggetti interessati.
- Per attivare eventuali processi di build e publish.
- Per rendere più semplice ad altre persone il contribuire al progetto, presentando una cronologia di commit meglio strutturata.
- Per generare i `CHANGELOG` automaticamente.

Tutto questo può farci risparmiare molto lavoro (e mal di testa) sia nel breve che nel lungo periodo e renderà chiara l' evoluzione del progetto anche a distanza di anni.
