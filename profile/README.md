<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/uchar-dev/.github/main/profile/hourglass-dark.png">
  <img alt="The uchar hourglass: RegelSpraak, Catala and F-logic translate into the uchar IR (spec, schema, verifier, corpus), which executes on Drools, Clingo (ASP) and a reference interpreter" src="https://raw.githubusercontent.com/uchar-dev/.github/main/profile/hourglass-light.png">
</picture>

## uchar — one intermediate language for executable law

*uchar* stands for **universal characteristic**, after Leibniz's *characteristica universalis*, scaled down from "all
human reasoning" to a domain where it can actually be built: legislation as executable rules.

Rules are written in a domain-specific language — RegelSpraak, Catala or F-logic today — and translated into one
intermediate representation whose meaning is fixed in a written specification. From that IR the same rules run on
Drools, on Clingo and on a reference interpreter. *n* languages and *m* engines meet in one waist: *n + m* translators
instead of *n × m*.

**Website: [uchar.dev](https://uchar.dev/?lang=en)** (English) · [Nederlands](https://uchar.dev/?lang=nl)

### Components

| | Component | What it does |
|---|---|---|
| **Waist** | IR specification | The product. Every well-formedness rule carries a `WF` number; the evaluation semantics come with worked examples that run verbatim as tests; JSON schemas and an OCaml verifier reject ill-formed documents before anything runs. |
| | Corpus | Golden cases with hand-computed expected values, negative documents the verifier must reject, and red cases that must fail observably in every executor. Built on the Jutterswet, an original, rights-free casus that mirrors the British Nationality Act experiment (Sergot et al., 1986). |
| **Source languages** | RegelSpraak | The controlled natural language in which the Dutch Tax Administration writes executable law, with GegevensSpraak for the data model. A Java parser and resolver emit the IR. |
| | Catala | Inria's language for tax law. It brought prioritized defaults — a general rule with exceptions — into the IR. |
| | F-logic | Class hierarchies with inheritable defaults as native frames; it keeps the inheritance kernel from being a RegelSpraak rendering. |
| **Executors** | Reference interpreter | A small OCaml interpreter that shares no code with the production runtime: the executable definition of the semantics. |
| | Clingo | Translation to ASP-Core-2, the semantically alien executor: stratified negation is a well-formedness condition of the IR, not an engine setting. |
| | Drools | The production rule engine on the JVM: an IR loader and two transpiler branches (DRL text and the executable model) over a shared runtime. |
| **Distribution** | RegelSpraak toolchain | CLI, embeddable engine, scenario runner and decision service (JDK `HttpServer` and Quarkus), packaged as a container image with a Helm chart. It has no semantics of its own: it builds uchar's RegelSpraak frontend and Drools backend at a pinned commit. |

The three executors share no code, and every corpus case must give the same hand-computed answer in all of them;
agreement between executors is never taken as truth by itself. Whatever an executor cannot carry, it refuses by name
and with a reason.

### Repositories

| Repository | Contents |
|---|---|
| `uchar` | The IR: specification, corpus, verifier, reference interpreter, frontends, backends and the gates that guard them |
| `regelspraak-toolchain` | The RegelSpraak distribution; carries `uchar` as a git submodule whose commit is the pin. Successor of `regelspraak-java` |
| `website` | The source of [uchar.dev](https://uchar.dev), static and bilingual |
| `research` | Research reports and assessments written alongside the work |

The repositories `uchar` and `regelspraak-toolchain` have been public since 12 October 2026; `website` and `research`
are private. The website is the public description of the project ([status](https://uchar.dev/?lang=en#status)).

### Reading on

- [Overview](https://uchar.dev/?lang=en) — what uchar is, why one intermediate language, and where it comes from
- [The languages](https://uchar.dev/talen.html?lang=en) — RegelSpraak, Catala and F-logic, and what each of them expresses
- [For the rule analyst](https://uchar.dev/regelanalist.html?lang=en) — from article to rule, scenario tests, explanations and the rule graph
- [For the DevOps engineer](https://uchar.dev/devops.html?lang=en) — the decision service: descriptor, container, endpoints, Kubernetes and runbook
- [Under the hood](https://uchar.dev/ontwikkelaar.html?lang=en) — specification, wire format, verifier, semantics, gates and roadmap

<sub>Code: Apache-2.0 · Specification and corpus: CC BY 4.0 · Maintained by Yeb Havinga</sub>
