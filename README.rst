Heat TileMill templates
-----------------------

Prep
~~~~
These images need heat-cfntools and cloudinit installed.

Create your ubuntu image as follows::

  mkdir where_i_build_images
  cd where_i_build_images
  git clone https://github.com/openstack/diskimage-builder.git
  git clone https://github.com/openstack/tripleo-image-elements.git

  TMP_DIR=~/tmp ELEMENTS_PATH=./tripleo-image-elements/elements:./diskimage-builder/elements ./diskimage-builder/bin/disk-image-create --no-tmpfs ubuntu vm heat-cfntools

Register your image with the following command::

  # I called mine "UR" for Ubuntu Raring
  glance add name=UR-x86_64-cfntools is_public=true disk_format=qcow2 container_format=bare < ubuntu-vm-heat-cfntools.qcow2


Create a keypair so you can login to the server::

  nova keypair-add heat_key > heat_key.priv
  chmod 600 heat_key.priv


Running
~~~~~~~

Run super-simple like::

  heat create simple -f super-simple.yaml -P "KeyName=heat_key;InstanceType=m1.small;ImageId=F19-x86_64-cfntools"

Run all_in_one like this::

  heat create inone -f all_in_one.yaml -e env.yaml -P "TileMillPassword=notthis;DBPassword=northis"

Status
~~~~~~
* The super-simple.yaml doesn't work for me as it doesn't seem to create
a DB.
* The all_in_one.yaml has some tilemill config error.

These might be because of the version of Ubuntu that I am using.
