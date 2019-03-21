# shiftstack-ci

Now that we are starting to move away from tripleo as a way to test ocp, this
repo is a tool to help you build and simplify your testing environment.

## Set up

Before running any of the scripts in this repo, there is minimal setup
required. First, make sure your go environment is functional, and if you don't
have a go environment set up, then set one up. [This guide has gifs of cats,
and is highly recommended if you are struggling with
this.](https://medium.com/@fsufitch/go-environment-setup-minus-the-insanity-b872f34351c8)
Next, make sure that you have a local copy of the clouds.yaml from your cloud
provider. You will need to clone the openshift installer, which can be found
[here](http://github.com/openshift/installer). Rather than clone using git, it
is much more convenient to use go get, since it will put it where it belongs
for you.

```bash
go get github.com/openshift/installer
```

Lastly, you need jq. This is easy, just run:

```bash
sudo dnf install jq
```

## Cluster Configuration


Make a copy of the `cluster_config.sh.example` file:

```shell
cp cluster_config.sh.example cluster_config.sh
```

Adjust the settings to match your environment. This will set up how and
where your cluster gets built, so it is important to fill it out carefully.
Here is a rundown of the important fields you will likely have to modify:

```
OS_CLOUD           The cloud in your openstack cluster that resources will be consumed from.
CLUSTER_NAME       What your ocp cluster will be nicknamed. This naming scheme is propogated to all resources in the cluster.
OPENSTACK_REGION   The cluster region that resources will be consumed from. For the moc, use moc-kzn
```

Once this has been set up, you are free to use the `run_ocp.sh` and
`destroy_cluster.sh` scripts.

## Building the Installer

Just run the convenience script: `build_ocp.sh`! You will have to do this
before your first run, and every time you make a change to the installer.

## Testing the Installer

This part is also pretty self-explanatory, the `run_ocp.sh` script will create
a cluster, and the `destroy_cluster.sh` script will destroy it. Moving
forwards, however, we will be looking to move away from building the cluster
this way, and towards using the CI tenant as our primary means of testing.
