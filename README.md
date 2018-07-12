# k8s

# ref https://github.com/dtzar/helm-kubectl/blob/master/README.md


Overview
This lightweight alpine docker image provides kubectl and helm binaries for working with a Kubernetes cluster. A local configured kubectl is a prerequisite to use helm per helm documentation. This image is useful for general helm administration such as deploying helm charts and managing releases. It is also perfect for any automated deployment pipeline needing to use helm which supports docker images such as Concourse CI, Jenkins on Kubernetes, Travis CI, and Circle CI. Having bash installed allows for better support for troubleshooting by being able to exec / terminal in and run desired shell scripts. Git installed allows installation of helm plugins.

If it is desired to only use kubectl and have kubectl as the entry command (versus this image as bash entry command), I recommend checking out this image instead: lachlanevenson/kubectl

Run
Example to just run helm on entry:
docker run --rm dtzar/helm-kubectl helm
By default kubectl will try to use /root/.kube/config file for connection to the kubernetes cluster, but does not exist by default in the image.

Example for use with personal administration or troubleshooting with volume mount for kubeconfig files:
docker run -it -v ~/.kube:/root/.kube dtzar/helm-kubectl
The -v maps your host docker machine Kubernetes configuration directory (~/.kube) to the container's Kubernetes configuration directory (root/.kube).

Build
For doing a manual local build of the image:
make docker_build

This image is now fully automated via travisci.org.
For reference this .travis.yml file can be validated via:
docker run --rm -it -v yourclonedreporoot:/project caktux/travis-cli lint ./travis.yml
