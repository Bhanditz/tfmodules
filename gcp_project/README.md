# gcp_project

Sets up a GCP project and ensures that a common set of SSH keys and
IAM users/roles are automatically enabled.

## Example

```
module "appsembler_infrastructure" {
  source = "github.com/appsembler/tfmodules//gcp_project?ref=gcp_project-0.2.0"
  name = "Appsembler Example"
  project_id = "appsembler-example"
  ssh_keys = "${file("ssh_keys.txt")}"
  owners = ["user1@noderabbit.com", "user2@noderabbit.com"]
  editors = ["user3@noderabbit.com", "user4@noderabbit.com"]
  domain = "noderabbit.com"
  services = ["compute.googleapis.com", "containerregistry.googleapis.com"]
}
```

## Variables

* `name` - name of the Project (required)
* `project_id` - project id to use. Currently required, but eventually
we will consider auto-generating this.
* `ssh_keys` - string containing all the SSH keys. One per line
  (newline separated), each line starts with `username:`. Also
  supports Google's extended syntax:
  https://cloud.google.com/compute/docs/instances/adding-removing-ssh-keys#sshkeyformat
  (if you want to set expiration times/etc.)
* `owners` - list of users to set as project owners. defaults to
  empty list.
* `editors` - list of users to set as project editors. defaults to
  empty list. May not overlap with `owners`.
* `domain` - domain to provide view access to. defaults to `noderabbit.com`
* `services` - list of service APIs to enable. Tip: `gcloud services
  list --project <yourproject>` will give the list of currently
  enabled ones.

## Outputs

* `project_id` - at the moment, this is kind of pointless since it's
  just the value that you've passed in, but in future, if we
  autogenerate the project id, this will be more useful.

## Releases

* `gcp_project-0.4.0` - use `google-beta` provider (should fix some quota problems)
* `gcp_project-0.3.1` - use `google_project_service` instead of `google_project_services`
* `gcp_project-0.3.0` - support services
* `gcp_project-0.2.0` - adds IAM setup
* `gcp_project-0.1.0` - initial version
