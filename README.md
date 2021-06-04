# OCP_Sample
Some examples

### Setup ###

Try login to registry by `docker login` or `podman login`.

Next create openshift secret from configuration file create from above login command.
```
oc create secret generic <pull_secret_name> \
    --from-file=.dockerconfigjson=<path/to/.docker/config.json> \
    --type=kubernetes.io/dockerconfigjson
```

Or you can create secret in openshift with username and password as follow:

```
oc create secret docker-registry <pull_secret_name> \
    --docker-server=<registry_server> \
    --docker-username=<user_name> \
    --docker-password=<password> \
    --docker-email=<email>
```

Now, Link pull secret for pulling images

```
oc secrets link default <pull_secret_name> --for=pull
```
