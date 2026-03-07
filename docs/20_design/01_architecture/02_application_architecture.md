# アプリケーションアーキテクチャ

本アプリケーションでは、**オニオンアーキテクチャ** を採用しています。

```mermaid
graph TD
    Presentation --> Application
    Application --> Domain
    Infrastructure --> Application
```

## CQRS と Mediator

- 読み取り（Query）と書き込み（Command）を分離する
- Application 層で UseCase を Command/Query として実装する
- MediatR 等のメディエーター（Mediator）を用いて、UI から UseCase 呼び出しを疎結合に保つ

```mermaid
graph TD
    UI[UI] -->|Command/Query| Mediator[Mediator]
    Mediator --> Cmd[Command Handler]
    Mediator --> Qry[Query Handler]
    Cmd --> Repo[Repository Port]
    Qry --> Repo
```
