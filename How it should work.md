- - -

We have frontends:
GUI , TUI , Phone, nintendo switch

We have the MASTER backend (hopefully `IBackend`)
which will be the core router / message bus

We have the DB
Something like `SQlite` , just to store & cache convos

and the Adapters
Sort of a 2 part solution because i want people to be able to write adapters in lua or python as well to make it easier for less hardcore people (and dum dums like me)
so part 1is something to turn that lua/py into understandable plugin code

part 2 is the actual backend adapter, which will have all the coms platforms!


## So taking all this in im thinking of:


| Concept basically analogy | type                              | What it will do                                                                                                                                                                    |
| ------------------------- | --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The actually logistics    | NeoIRC System component           | Responsibilities & design hehe                                                                                                                                                     |
| Standard containers       | like `Universal message`          | Messages coming from anywhere are re-wrapped in a universal format                                                                                                                 |
| Adapters                  | backend modules                   | The actuall raw protocol interfaces. So basically a IRC module just handles raw text streams but a Discord module translates HTTP/WebSocket frames, all output `Universal message` |
| Sorter                    | Core event bus thing              | Basically receives `Universal messageS` for everything and tags them with a global id or some sort, sticks them in the ledger and routes them to the frontend / DB                 |
| Database                  | `SQLite should do`                | Stores everything , and should allow for a query interface api so frontend can do "Show me all `universal message` thats delivered to `#general` in the last day"                  |
| Frontend                  | TUI or just an `IFrontend` Driver | Presents a message UI to the end-user. doesnt care about the rest of the chain, just talks with the DB                                                                             |
