# tfmodules

Reusable Terraform Modules

## Conventions

Each module should be in its own directory.

Each module directory should contain a README documenting variables,
outputs, and showing some sample code.

Variables should be split out into `variables.tf` and outputs into
`outputs.tf`. Group other resources together however you think is
reasonable. For a very small, simple state, it might be fine to put
everything in one `main.tf`. For a larger one, you might want to split
it by resource type.

If a resource supports tags or labels, add a `Terraform = true`
label/tag on it (this makes it easier for us to see what resources are
managed by terraform when we're in a console).

## Tags/Versions

Create independent tags for each module. Eg,

```
$ git tag health-check-0.1.0
$ git push origin --tags
```

So that module can then be used as
`github.com/appsembler/tfmodules//health_check?ref=health-check-0.1.0`. This
is a little odd, but necessary since these modules all live in the
same github repo but should be independantly versioned.
