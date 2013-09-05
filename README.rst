Heat TileMill templates
-----------------------

Run super-simple like::

  heat create simple -f super-simple.yaml -P "KeyName=heat_key;InstanceType=m1.small;ImageId=F19-x86_64-cfntools"

Run all_in_one like this::

  heat create inone -f all_in_one.yaml -e env.yaml -P "TileMillPassword=notthis;DBPassword=northis"
