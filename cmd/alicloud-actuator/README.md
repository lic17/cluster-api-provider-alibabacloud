# Alibabacloud actuator

The command allows to directly interact with the alibabacloud actuator.

## To build the `alibabacloud-actuator` binary:

```sh
$ make alibabacloud-actuator
```

## Prerequisities

All the machine manifests assume existence for various Alibabacloud resources such as vpc,
security groups, etc. :

## Create Alibabacloud ECS instance based on machine manifest

The `examples/userdata.yml` secret encodes the following user data:
```sh
#!/bin/bash
echo "Hello Alibaba" > /tmp/test
```

The environment variables  `ALICLOUD_ACCESS_KEY_ID` and `ALICLOUD_ACCESS_KEY_SECRET`  must  to be set.

```sh 
$ export ALICLOUD_ACCESS_KEY_ID=<YOUR_ALICLOUD_ACCESS_KEY_ID>
$ export ALICLOUD_ACCESS_KEY_SECRET=<YOUR_ALICLOUD_ACCESS_KEY_SECRET>

```

```sh
$ ./bin/alibabacloud-actuator create --logtostderr -m examples/machine-with-user-data.yaml -u examples/userdata.yml
Machine creation was successful! InstanceID: i-bp117zgballjltfnl3up```

Once the alibabacloud instance is created you can run `$ cat /tmp/test` to verify it contains the `Ahoj` string.

## Test if alibabacloud instance exists based on machine manifest

```sh
$./bin/alibabacloud-actuator exists --logtostderr -m examples/machine-with-user-data.yaml -u examples/userdata.yml
I0815 11:15:30.875728   45782 actuator.go:389] alibabacloud-actuator-testing-machine: Checking if machine exists
I0815 11:15:31.514626   45782 actuator.go:402] alibabacloud-actuator-testing-machine: Instance exists as "i-bp117zgballjltfnl3up"
Underlying machine's instance exists.
```

## Delete alibabacloud instance based on machine manifest

```sh
$ ./bin/alibabacloud-actuator delete --logtostderr -m examples/machine-with-user-data.yaml 
I0815 11:16:10.242073   45838 utils.go:171] Cleaning up extraneous instance for machine: i-bp117zgballjltfnl3up, state: Running, launchTime: 2019-08-15T02:43Z
Machine delete operation was successful.
```

