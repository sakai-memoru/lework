# JSON Server Usage

## Overview

- Mock用APIサーバ
  + サンプルデータ（json）にて構築。
  + 簡単なrequest - responseを提供。

## reference
- GitHub
  + https://github.com/typicode/json-server

- 【個人メモ】JSON Serverを使って手っ取り早くWebAPIのモックアップを作る
  + https://qiita.com/futoase/items/2859a60c8b240da70572

## Installation

- node.jsをinstall
  + https://nodejs.org/ja/download/

- json serverをinstall

- 以下、操作例

```powershell
PS G:\> node --version
v6.9.1
PS G:\> npm --version
3.10.8
PS G:\> npm install -g json-server
G:\Users\sakai\AppData\Roaming\npm\json-server -> G:\Users\sakai\AppData\Roaming\npm\node_modules\json-server\bin\index.js
G:\Users\sakai\AppData\Roaming\npm
`-- json-server@0.14.0
  +-- body-parser@1.18.3
  +-- chalk@2.4.1
  +-- compression@1.7.2
  +-- connect-pause@0.1.1
  +-- cors@2.8.4
  +-- errorhandler@1.5.0
  +-- express@4.16.3
  +-- express-urlrewrite@1.2.0
  +-- json-parse-helpfulerror@1.0.3
  +-- lodash@4.17.10
  +-- lodash-id@0.14.0
  +-- lowdb@0.15.5
  +-- method-override@2.3.10
  +-- morgan@1.9.0
  +-- nanoid@1.0.3
  +-- object-assign@4.1.1
  +-- please-upgrade-node@3.0.2
  +-- pluralize@7.0.0
  +-- request@2.87.0
  +-- server-destroy@1.0.1
  +-- update-notifier@2.5.0
  `-- yargs@10.1.2

PS G:\>
```
- check installation

```powershell
PS G:\> $Env:path.split(";") | Out-String -Stream | sls npm

G:\Users\sakai\AppData\Roaming\npm

PS G:\> json-server
index.js [options] <source>

Options:
  --config, -c               Path to config file   [default: "json-server.json"]
  --port, -p                 Set port                            [default: 3000]
  --host, -H                 Set host                     [default: "localhost"]
  --watch, -w                Watch file(s)                             [boolean]
  --routes, -r               Path to routes file
  --middlewares, -m          Paths to middleware files                   [array]
  --static, -s               Set static files directory
  --read-only, --ro          Allow only GET requests                   [boolean]
  --no-cors, --nc            Disable Cross-Origin Resource Sharing     [boolean]
  --no-gzip, --ng            Disable GZIP Content-Encoding             [boolean]
  --snapshots, -S            Set snapshots directory              [default: "."]
  --delay, -d                Add delay to responses (ms)
  --id, -i                   Set database id property (e.g. _id) [default: "id"]
  --foreignKeySuffix, --fks  Set foreign key suffix (e.g. _id as in post_id)
                                                                 [default: "Id"]
  --quiet, -q                Suppress log messages from output         [boolean]
  --help, -h                 Show help                                 [boolean]
  --version, -v              Show version number                       [boolean]

Examples:
  index.js db.json
  index.js file.js
  index.js http://example.com/db.json

https://github.com/typicode/json-server

Missing <source> argument
PS G:\> json-server --version
0.14.0

```

## Usage

- 1. サンプルデータをもとに、json-serverを起動

```powershell
PS G:\> json-server G:\apps_data\le\tcmp\json\sample.json

  \{^_^}/ hi!

  Loading G:\apps_data\le\tcmp\json\sample.json
  Done

  Resources
  http://localhost:3000/jobs
  http://localhost:3000/users

  Home
  http://localhost:3000

  Type s + enter at any time to create a snapshot of the database

```
- access : http://localhost:3000


- 2. Browserでアクセス

  http://localhost:3000/jobs   ・・・案件データ
  http://localhost:3000/users  ・・・json server用サンプルデータ

- home http://localhost:3000
![json server home](https://i.imgur.com/hzkhKff.png)

- http://localhost:3000/jobs
![json server jobs](https://i.imgur.com/Thfyp3M.png)

- http://localhost:3000/jobs/?seq_id=9010
![json server jobs/?seq_id=9010](https://i.imgur.com/QvMSL3c.png)

- 3. curlでアクセス

```powershell
PS G:\Users\sakai> curl -uri http://localhost:3000/users/


StatusCode        : 200
StatusDescription : OK
Content           : [
                      {
                        "id": "1",
                        "name": "Leading Me"
                      },
                      {
                        "id": "2",
                        "name": "sample"
                      },
                      {
                        "id": "3",
                        "name": "Leading Edge"
                      },
                      {
                        "name": "Leading",
                        "id": "rEOJAfi"
                      }
                    ]
RawContent        : HTTP/1.1 200 OK
                    Vary: Origin, Accept-Encoding
                    Access-Control-Allow-Credentials: true
                    Pragma: no-cache
                    X-Content-Type-Options: nosniff
                    Connection: keep-alive
                    Content-Length: 199
                    Cache-Control: n...
Forms             : {}
Headers           : {[Vary, Origin, Accept-Encoding], [Access-Control-Allow-Credentials, true], [Pragma, no-cache],
                    [X-Content-Type-Options, nosniff]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 199

```

// --- end of file
