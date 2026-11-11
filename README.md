# Feature Flags

The common feature-flag vocabulary -- the flags that switch features, the environments they are switched in, the segments they target and the experiments run on them -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Feature Flags, Feature Management, Experimentation, A/B Testing, Feature Toggles, Progressive Delivery in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| flag | 19 | 19 | name 79%, description 74%, enabled 68%, id 68%, key 68%, metadata 63%, created_at 53%, type 53% | flags 12, features 4, feature-flags 2, feature_flags 2 |
| flag_environment | 11 | 11 | name 91%, id 82% | environments 10, environment 2 |
| flag_segment | 9 | 9 | description 100%, id 100%, name 100%, created_at 67%, rules 67% | segments 5, cohorts 3, audiences 3, segment 1 |
| experiment | 7 | 7 | id 100%, name 100%, description 86%, status 86%, created_at 57%, ended_at 57%, started_at 57% | experiments 7 |

Cohort: 36 providers with harvested OpenAPI, 19 crosswalks. Of the providers exposing a flag: 90% create, 79% list, 79% fetch, 79% update, 63% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A flag agrees on key, name, description, whether it is enabled, its type and created_at -- feature-flag platforms, experimentation tools and identity providers with flags (Statsig's gates, PostHog, Kinde) share the toggle's shape almost completely.
- Segments agree on name, description and rules; experiments on status, start and end -- the targeting and the test share a shape as well as the flag.
- The cohort is small (36 providers, 19 mapped): most flag platforms deliver flags through SDKs and keep the management API secondary.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [arazzo.yml](arazzo.yml) -- reference workflows composed only of the shared operations (compositions, not measurements).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Gates, toggles and switches are flags; features count as flags only beneath a project or environment (a bare `/features` is a product's feature list elsewhere).
- Environments are `/flag-environments` and segments `/flag-segments`: CI/CD owns `/environments` and analytics owns cohorts. Audiences and cohorts count as flag segments only at a provider that also serves flags.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
