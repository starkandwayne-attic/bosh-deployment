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


Jurassic BOSH
======================================

Jurassic BOSH is a paradigm for deploying multiple BOSH directors to eliminate
much of the time-sink created by `bosh-init`. Its highly useful in a situation
where you have many BOSH directors (one for each of your staging, prod, dev, etc.
environments). Essentially, you deploy a Proto BOSH via `bosh-init`, and then
deploy the environment-specific BOSHes on top of your Proto BOSH as regular
BOSH deployments.

Doing this with these templates is quite easy! To stand up your Proto BOSH:

```
$ genesis new deployment --template bosh
$ cd bosh-deployments
$ genesis new site --template <aws|vsphere|openstack> site-name
$ genesis new env --type bosh-init site-name proto
$ cd site-name/proto
$ make deploy # ... and fill in all the required parameters to deploy your BOSH
```

Once that bosh has been stood up, you can target it with the BOSH cli, and
start creating your environment-specific BOSHen:

```
$ bosh target https://your.director.ip:25555 site-name-proto-bosh
$ genesis new env --type normal site-name staging
$ cd ../staging # assuming you were still in the site-name/proto directory
$ make deploy # ... and fill in all the required parameters to deploy your BOSH
```

The deployment in `site-name/proto` will get deployed via `bosh-init`, while the
`site-name/staging` deployment will be deployed via BOSH against the `site-name-proto-bosh`
director. As of now, the `--type normal` flag is optional for regular BOSHen, since it
is the default method for deploying in `genesis`


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

Microsoft Azure (Azure) Sites
======================================

The `azure` template will set you up with a structure suitable for
deploying BOSH directors to Azure's ARM
infrastructure.

    genesis new site --template azure <name>


Google Cloud Platform (Google) Sites
======================================

The `google` template will set you up with a structure suitable for
deploying BOSH directors to Google Cloud Plaftorm infrastructure.

    genesis new site --template google <name>



vCloud Director (vCloud) Sites
======================================

The `vcloud` template will set you up with a structure suitable for
deploying BOSH directors to vCloud Director infrastructure.

    genesis new site --template vcloud <name>



Notes
======================================

For more information, check out the [Genesis][1] repo, or `genesis help`.
You can download the Genesis program from [Github][1]



[1]: https://github.com/starkandwayne/genesis
