BOSH Deployment Template
======================================

This repository acts as an upstream repository of YAML templates for use
in deploying one or more BOSH directors, via the [Gensis][1] utility.



Creating a new BOSH Deployment
======================================

To create a new [Genesis][1]-based deployment of BOSH, run

    genesis new deployment --template bosh

This will create a new repo called `bosh-deployments` for you, and
pull in the `github.com/starkandwayne/bosh-deployment` repo as the
`upstream` remote, copying the contents of `global/*` into the new
`bosh-deployments` repository.

This allows you to easily diverge from the upstream templates to suit your
environment, yet still be able to pull in changes from upstream down
the road.



vSphere Sites
======================================

The `vsphere` template will set you up with a structure suitable
for deploying BOSH directors on a VMWare vSphere ESXi cluster.

    genesis new site --template vsphere <name>



Amazon EC2 (AWS) Sites
======================================

The `aws` template will set you up with a structure suitable for
deploying BOSH directors to Amazon Web Service's EC2/VPC
infrastructure.

    genesis new site --template aws <name>



Notes
======================================

For more information, check out the [Genesis][1] repo, or `genesis help`.
You can download the Genesis program from [Github][1]



[1]: https://github.com/starkandwayne/genesis
