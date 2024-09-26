# Steps

You are subgraph admin for the `analytics` and `sales` subgraphs.

## Set the project

Use the project name provided by the supergraph admin.

`ddn context set project <project-name>`

## Test locally

```bash
ddn supergraph build local
ddn run docker-start
```

## Add cross subgraph relationships

```bash
git merge feature_cross_subgraph_relationships
```

## Deploy to DDN

```bash
ddn subgraph build create --subgraph sales/subgraph.yaml
ddn subgraph build apply <version> # from the previous command
```