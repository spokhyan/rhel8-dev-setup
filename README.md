# rhel8-dev-setup

Follow given steps to setup a new RHEL machine for Java Developers

Install Java/JDK
you can install jdk 8 and 11 individually or together. Access Terminal and run following command -

Install indivisually 

For JDK 8 :
sudo yum install java-1.8.0-openjdk-devel

For JDK 11 :
sudo yum install java-11-openjdk-devel


install together : JDK 8, 11 and maven

sudo yum install java-1.8.0-openjdk-devel java-11-openjdk-devel maven

Selecting Java Versions with Alternatives

alternatives --list

sudo alternatives --config java

Enter to keep the current selection[+], or type selection number: 2

sudo alternatives --config javac

Switching alternatives non-interactively

$ JAVA_11=$(alternatives --display java | grep 'family java-11-openjdk' | cut -d' ' -f1)
$ sudo alternatives --set java $JAVA_11

Similarly, switching to JDK 8 via alternatives by non-interactive means:

$ JAVA_8=$(alternatives --display java | grep 'family java-1.8.0-openjdk' | cut -d' ' -f1)
$ sudo alternatives --set java $JAVA_8

Selecting Java Versions by Setting JAVA_HOME

Installing the Openshift CLI by using an RPM

For Red Hat Enterprise Linux (RHEL), you can install the OpenShift CLI (oc) as an RPM if you have an active OpenShift Container Platform subscription on your Red Hat account.



    Register with Red Hat Subscription Manager:

    # subscription-manager register

    Pull the latest subscription data:

    # subscription-manager refresh

    List the available subscriptions:

    # subscription-manager list --available --matches '*OpenShift*'

    In the output for the previous command, find the pool ID for an OpenShift Container Platform subscription and attach the subscription to the registered system:

    # subscription-manager attach --pool=<pool_id>

    Enable the repositories required by OpenShift Container Platform 4.3.

        For Red Hat Enterprise Linux 8:

        # subscription-manager repos --enable="rhocp-4.3-for-rhel-8-x86_64-rpms"

        For Red Hat Enterprise Linux 7:

        # subscription-manager repos --enable="rhel-7-server-ose-4.3-rpms"

    Install the openshift-clients package:

    # yum install openshift-clients

After you install the CLI, it is available using the oc command:

$ oc <command>

Install Buildah, Skopeo, and Podman

# yum -y install buildah skopeo podman

Setup Local OpenShift 4.7 Cluster with CodeReady Containers

    It uses a single node which behaves both as a master and as a worker node.
    The machine-config and monitoring Operators are disabled by default.
    These disabled Operators will cause the corresponding parts of the web console to be non functional.
    For the same reason, there is currently no upgrade path to newer OpenShift versions.
    Due to technical limitations, the CodeReady Containers cluster is ephemeral and will need to be recreated from scratch once a month using a newer release.
    The OpenShift instance is running in a virtual machine, which could cause some other differences, in particular in relation with external networking.
    
# Step 1: Install required software packages
sudo yum -y install qemu-kvm libvirt virt-install bridge-utils NetworkManager
sudo systemctl enable --now libvirtd 

# Step 2: Install CodeReady Containers

wget https://mirror.openshift.com/pub/openshift-v4/clients/crc/latest/crc-linux-amd64.tar.xz




