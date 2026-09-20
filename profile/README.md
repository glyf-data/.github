# glyf

**Open source visualisation build tool for the data pipeline.**

`glyf` lets analytics engineers define charts in SQL, next to the models those
charts read from. Chart definitions live in `.ggsql` files, move through code
review like any other code, and compile into versioned artifacts — PNG, SVG,
Vega JSON, and static dashboard sites — with no BI server anywhere in the loop.

`glyf` is **artifact-driven, not runtime-driven**. It reads the metadata your
transformation tool already produces — starting with dbt's `manifest.json`,
resolving `ref()` and `source()` from it — executes the chart SQL, and writes
deterministic output you can inspect, diff, archive, and publish anywhere.

```sql
SELECT week, plan, sum(activated_users) AS activated_users
FROM {{ ref('fct_product_usage') }}
GROUP BY 1, 2

VISUALISE week AS x, activated_users AS y, plan AS color
DRAW line
LABEL title => 'Activation by Plan'
INTERACT tooltip, legend_filter
```

```bash
dbt build      # your models, unchanged
glyf build     # charts, dashboards, static site
glyf serve     # local preview
```

The chart syntax builds on [ggsql](https://ggsql.org), which brings Grammar of
Graphics clauses — `VISUALISE`, `DRAW`, `SCALE`, `LABEL` — into SQL workflows.

## Projects

| Repository | Description | Language |
| --- | --- | --- |
| [glyf](https://github.com/glyf-data/glyf) | The `glyf` CLI, the `.ggsql` chart compiler, and the dashboard generator | Python, Rust |

## Get started

```bash
uv tool install glyf-core   # PyPI package is glyf-core; the command is glyf
glyf --version
```

Wheels ship for Linux, macOS, and Windows on Python 3.11+. Other options are in
the [installation guide](https://glyfdata.com/docs/get-started/installation).

Then follow the [Quickstart](https://glyfdata.com/docs/get-started/quickstart)
to scaffold your first chart, or
[Existing dbt project](https://glyfdata.com/docs/get-started/existing-dbt-project)
to add `glyf` to a repo you already have.

## Resources

- **Documentation** — <https://glyfdata.com/docs>
- **Examples gallery** — <https://glyfdata.com/docs/examples/gallery>
- **Issues** — <https://github.com/glyf-data/glyf/issues>
- **Discussions** — <https://github.com/glyf-data/glyf/discussions>

## Contributing

Pull requests, bug reports, and thoughtful issues are welcome. Start with
[CONTRIBUTING.md](https://github.com/glyf-data/glyf/blob/main/CONTRIBUTING.md),
and see [GOVERNANCE.md](https://github.com/glyf-data/glyf/blob/main/GOVERNANCE.md)
for how decisions get made.

## Governance and legal

Projects in this organisation follow the
[Contributor Covenant Code of Conduct](https://github.com/glyf-data/glyf/blob/main/CODE_OF_CONDUCT.md),
version 2.1.

Licensed under [Apache License 2.0](https://github.com/glyf-data/glyf/blob/main/LICENSE).

Please report security vulnerabilities privately through
[GitHub security advisories](https://github.com/glyf-data/glyf/security/advisories/new)
rather than in a public issue.
