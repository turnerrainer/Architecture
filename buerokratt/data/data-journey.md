### Use case nr 1 - End Client gets their response from Rasa

```mermaid
sequenceDiagram
  participant Client
  participant Widget
  participant Ruuter
  participant Rasa
  participant RelationalDB
  participant NoSQL
  participant SSE

  autonumber
  Client->>Widget: Tere
  Widget->>Ruuter: Tere
  Ruuter->>Rasa: Tere
  Rasa-->>Ruuter: Tere. Kuidas saan teid aidata?
  Ruuter->>RelationalDB: Tere. Kuidas saan teid aidata?

  loop Continuously fetch for new messages
    loop Check for new message notifications
      SSE->>NoSQL: New messages?
      NoSQL-->>SSE: Boolean true/false
      note over Widget,SSE: Notify Widget when it should initiate a request to fetch new messages
      SSE->>Widget: *There are new messages for Chat ID XYZ*
    end

    Widget->>Ruuter: *Send new messages for Chat ID XYZ*
    Ruuter->>Resql: *Send new messages for Chat ID XYZ*
    Resql-->>Ruuter: Tere. Kuidas saan teid aidata?
    Ruuter-->>Widget: Tere. Kuidas saan teid aidata?
  end
  
  Widget-->>Client: Tere. Kuidas saan teid aidata?
```
