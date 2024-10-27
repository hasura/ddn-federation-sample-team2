**Context: You have been invited to DDN Project by the owner of a supergraph (Team1)**

You are subgraph admin for the `sales` subgraphs/domain.

1. Go to hasura.console.io and accept the invite and expore the experience subgraph by Team1
2. Go to Settings in the console and copy the project name.
3. `ddn context set project <project-name>`
4. Test locally
If you are starting from scratch you would use the following two commands, but that work is already done in this example repo.

```bash
## ddn subgraph init sales --dir ./sales
## ddn subgraph add --subgraph ./sales/subgraph.yaml --target-supergraph ./supergraph.yaml
```

5. `ddn supergraph build local`
6. `ddn run docker-start`

## DDN Advanced CI/CD

1. Create Subgraph Build
```bash
ddn subgraph build create --subgraph sales/subgraph.yaml
# ddn subgraph build create --subgraph sales/subgraph.yaml --no-build-connectors
```

2. Go to Console - Subgraph builds appear

![alt text](images/subgraphbuild.png)

But you still need one more step to test

1. `ddn supergraph build create --subgraph-version sales:<version_number>`
Here DDN does a cross repo (subgraph) check to ensure that there are no breaking changes to the larger API

This is a signficant milestone since the subgraph developer is able to push to Team1 project

1. Go to Console -explorer - sales subgraph is added
2. Add a comment on the userid in Coupon table for a multi repo relationship
3. Add the following multi repo relationship in file `.hml`
    ```yaml
    kind: Relationship
    version: v1
    definition:
    name: products
    source: Orders
    target:
        model:
        name: Products
        subgraph: experience
        relationshipType: Object
    mapping:
        - source:
            fieldPath:
            - fieldName: productId
        target:
            modelField:
            - fieldName: id
    ```

`ddn subgraph build apply <version> # from the previous command`


## Add cross subgraph relationships

```bash
git merge feature_cross_subgraph_relationships
```