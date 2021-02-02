![AWS Bundle](https://github.com/mikthoma/ocpag-repo/workflows/AWS%20Bundle/badge.svg?branch=main)

Openshift 4 Offline Bundle Generation Tool
=========

Generates a Bundle for desired cloud, execution platform, and version. This is used to aggregate dependencies from all of the various Red Hat official resources.

Pre-Generated Bundles
--------------

![AWS Bundle](https://github.com/mikthoma/ocpag-repo/workflows/AWS%20Bundle/badge.svg?branch=main)  [Download Link](https://ocpagpkg.s3-us-west-1.amazonaws.com/aws/openshift4-linux-4.6.8-x86_64.tar.gz) | [sha256sum](https://ocpagpkg.s3-us-west-1.amazonaws.com/aws/sha256sum.txt)


Playbook Variables
--------------

| Variable | Options | Description | Default Value |
|--|--|--|--|
| **cloud_selection** (*string*) | *aws, gcp, openstack, azure, vmware, metal* | Selects the appropriate target image to download from the latest releases image repository. | aws |
| **destination** (*string*) |  | Local path where you want the image to be saved. Can be a directory, or an absolute file path. |  |
| **os_platform** (*string*)| *linux, macos, windows* | Which type of operating system you want to download binaries such as *oc* and *openshift-install* for. | linux |
| **ocp_version** (*string*)|  | Version of Openshift to target for pulling dependencies | 4.6.8 |
| **pull_secret_path** (*string*) |  | Path to your pull secret file, which can be obtained in the Red Hat Cluster Manager website. |  |

Use Guide
--------------

Recommended: Write desired values to a variables YAML file, then input through `--extra-vars`.

```
cat > my_variables.yml << EOF
cloud_selection: aws
destination: /my/destination/folder
os_platform: linux
ocp_version: "4.6.8"
pull_secret_path: /home/user1/pull_secret.txt
EOF

ansible-playbook generate.yml --extra-args "@my_variables.yml"
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'

PLAY [Generate Openshift Bundle] ***********************************
```

Alternative: Run the playbook as needed, and provide the inputs to the prompts.

```
➜  ansible-playbook generate.yml
[WARNING]: provided hosts list is empty, only localhost is available. Note that the implicit localhost does not match 'all'
Desired path to dump content (example: /home/user1/bundle): /home/user1/folder
Cloud to generate content for (aws,gcp,azure,metal,vmware,openstack) [aws]: 
Path to your Pull Secret file (example: /home/user1/pull_secret.txt): /home/user1/pull_secret.txt
Desired Operating System Platform for execution (linux,macos,windows) [linux]: 
Desired Openshift Version [4.6.8]: 

PLAY [Generate Openshift Bundle] ***********************************
```
