# Full Stack Data Engineer Toolkit

Canonical data pipelines in a universal language, plus a spec driven development system built for use with an AI code assistant: you write the spec, and the assistant turns it into an implementation on the system you choose.

This toolkit is built for data engineers. It is a companion for the whole career path: you build as you learn, each pipeline teaches the design behind it while you implement it, and the specs and mappings you write along the way stay in the toolkit as assets for the next problem. Over time, it grows into your library of proven designs.

The designs come from production work across specific industries, but they are generalised so they apply in any industry.

## Start here

| You want to | Go to |
|---|---|
| Solve a real problem, end to end | A pipeline in `pipelines/` |
| Implement a design on your system | `spec-driven-development/`: a spec, its mapping, and the skill |
| See everything the toolkit covers | The coverage map below |

## Pipelines

Each pipeline is a complete, real world flow. Its folder holds the design (README), the story behind it (post), its stages in spec form (spec) and its evals: sample inputs with the expected outputs. Status shows maturity: draft, reviewed, or production verified, and production verified is earned by passing evals on that system, never claimed without them.

| Pipeline | What it does | Status |
|---|---|---|
| Email metrics | Raw events to a denormalized table to a metrics table | Planned, first build |
| Revenue attribution | Touchpoints connected to revenue, reconciled with finance | Planned |
| Event unification | Email, in game and web events joined into one journey | Planned |
| Audience | Audiences defined once and activated across channels | Planned |
| Experimentation | Tests, holdouts and readouts built into the platform | Planned |

Work is built in vertical slices: one pipeline end to end first, with only the use cases and mapping rows it needs, on one target system. The email metrics pipeline on AWS is the first slice.

## Spec driven development

Pipelines are written in universal language: concepts such as source, table, partition and schedule, defined once in a vocabulary. Cloud and tool names appear in exactly one place, the mappings. System, throughout this repo, means the target you implement on: a cloud such as AWS, or a platform such as Snowflake that runs on a cloud.

Inside `spec-driven-development/`:

| Part | What it holds |
|---|---|
| Vocabulary | Every universal term, defined once, with an example |
| Use cases | One module per capability, written as a spec: inputs, outputs, rules, configuration, guarantees, evals |
| Mappings | One file per target system: this universal term, on this target, is this service. AWS is the first target |
| Evals | The runnable checks every spec carries: a fixture input, an action, the expected result, and a pass rule. Stage evals gate each step of an implementation; end to end evals confirm the finished pipeline |
| Skills | One skill, implement-spec: it reads a spec and a target, applies that target's mapping, produces the implementation, and runs the evals stage by stage before proceeding |

Pipelines are assembled from use cases. Each stage of a pipeline points to the use case that does that job: the email metrics pipeline, for example, points to deduplication for its dedupe stage, instead of describing deduplication again inside the pipeline. When a pipeline needs something no use case covers yet, that something is written as a new use case first, and only then used by the pipeline. Each mechanic is defined once, in its use case, and every pipeline reuses that single definition.

### Using it with an AI code assistant

This is the intended way to work with the toolkit:

1. Clone the toolkit next to your own project, or copy the parts you need into it.
2. Open your AI code assistant in that workspace and point it at a pipeline spec and a target system, for example: implement the email metrics pipeline on AWS.
3. The assistant reads the vocabulary and the use case specs the pipeline names, looks each universal term up in the target's mapping, and follows the implement-spec skill to generate the implementation.
4. Anything the mapping does not cover, the assistant reports as a gap instead of guessing. You decide the mapping, and the spec grows.
5. After each stage, the assistant runs that stage's evals and proceeds only when they pass. A failed eval stops the run and is reported, with the stage unfinished. When the pipeline is complete, its end to end evals confirm the result is what the spec promised.
6. You review the generated code and the eval results, the same review you would give any implementation.
7. Close the loop. After each implementation, write down the issues it exposed: a rule the spec stated badly, a term the mapping got wrong, a step where the assistant had to stop and ask. Then improve the instructions themselves: fix the spec, correct the mapping, sharpen the skill. When a bug escapes the evals, a new eval is written for it. The next implementation runs faster and lands better because the instructions learned from the last one.

That is why specs here are written the way they are: inputs, outputs, rules, configuration, guarantees and evals, stated precisely in a fixed template. A spec has two readers, you and your assistant, and it has to be exact for both. The design decisions stay with the engineer; the assistant carries them into code, one system at a time. And the feedback loop runs after every implementation, so the instructions keep improving with real use.

First use case families: data ingestion, data transform, data export, permissions, infra and storage.

## Coverage map

The toolkit covers the full stack a staff data engineer is expected to own:

| Area | What it covers |
|---|---|
| Capture and ingestion | Batch, streaming, CDC, APIs, event instrumentation and taxonomy |
| Storage and lakehouse | Warehouse and lake design, table formats, partitioning, retention, cost |
| Transformation and orchestration | SQL and Python pipelines, scheduling, backfills, idempotency, late and restated data |
| Quality, observability and governance | Data quality checks, freshness and volume monitoring, lineage, catalog |
| Customer identity, privacy and consent | Identity resolution, PII handling, consent enforcement, privacy regulation such as LGPD, GDPR and CCPA |
| Modeling and semantics | Conformed dimensions, metrics layer, one definition used everywhere |
| Serving and activation | BI, APIs, reverse ETL, audience and campaign platforms |
| Measurement and learning | Attribution, experimentation, holdouts, incrementality |
| Infrastructure | Cloud accounts and projects, networking, compute and storage provisioning, infrastructure as code, environments, deployment pipelines, cost management |
| Identity, permissions and security | IAM roles and policies, service identities, least privilege access, data access rules per team and per role, secrets management, encryption, audit logging |

## Repo structure

```text
full-stack-data-engineer-toolkit/
├── README.md                    This file
├── pipelines/                   Canonical pipelines, each with design,
│                                story, spec, evals, and an optional
│                                examples/ snapshot of a generated
│                                implementation
├── spec-driven-development/     Vocabulary, use case specs, mappings
│                                (one file per target system), and the
│                                implement-spec skill
└── templates/                   Spec template, RFC, data contract,
                                 design review, experiment readout,
                                 incident review
```

Folders are created when their first file is written, one piece at a time.

## Contributing

Contributions are welcome. Corrections, examples from other industries or systems, and questions that expose a gap are all useful. The project is young, so please open an issue first for anything larger than a small fix.

## Contributor

Maintained by Renan Sallai Iwayama, [@rsallaii](https://github.com/rsallaii) on GitHub, [rsallaii](https://www.linkedin.com/in/rsallaii) on LinkedIn

---

*Status: just starting. This README is the first file. Updated 9 Nov 2026.*
