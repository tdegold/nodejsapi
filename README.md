# A simple node API
Tim Degold, begonnen am 07.11.2020

Dieses Projekt ist eine einfache API, welche mit *nodejs* und *express* realisiert wird. ZUguterletzt wird sie in einem docker-container isoliert, damit reibungsloses deployment garantiert wird.

## API
Die API stellt (zu Beginn) nur einen Endpoint zur Verfügung, welcher `Hello, World!` ausgibt [2].

```javascript
app.get('/', (req, res) => {
  res.send('Hello World!')
});
```

Die API wird auf `localhost` auf Port `8000` laufen.

```javascript
app.listen(port, () => {
  console.log(`Example app listening on  http://localhost:${port}`)
});
```

Wenn man die App nun mit `node index.js` startet, wird die Meldung im Browser korrekt angezeigt.

![helloworld](img/helloworld.png)

## docker-compose
In `package.json` wird ein script hinzugefügt, mit welchem mann die API startet [3].

```json
...
"scripts": {
    "start": "node index.js"
  },
...
```

Nun kann das docker-compose aufgebaut werden [1]. `expose` wird zu `ports`, damit auch über `localhost` auf die API zugegriffen werden kann.

```yml
# before
expose:
  - "8000"
# after
ports:
  - "8000:8000"
```

Nun kann die API mit `docker-compose up [-d]` aufgerufen werden und die API ist wieder über Port `8000` erreichbar.

## git clone
Wenn man an diesem Projekt weiterarbeiten möchte kann man es mit `git clone` leicht kopieren. Nun einfach mit `npm install` die Dependencies herunterladen und entweder mit 
- `npm run start`
- `node index.js`

oder

- `docker-compose up [-d]`

starten. Viel Spaß!


## Quellen
[1] *nodejs docker image doc* https://github.com/nodejs/docker-node/blob/master/README.md#how-to-use-this-image [zugegriffen 07.11.2020]

[2] *express.js doc* https://expressjs.com/de/4x/api.html [zugegriffen 07.11.2020]

[3] *setup npm environment* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/development_environment [zugegriffen 07.11.2020]

[4] *untrack certain files in git* https://gist.github.com/ginfuru/c4eeb594759056b1df05c39af61b1a27 [zugegriffen 07.11.2020]