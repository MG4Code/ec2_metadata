# Retrieving EC2 instance metadata to import to systemd

## Using python
To retrieve EC2 insntances information, we can query that information through instance metadata endpoint. (http://169.254.169.254/latest/meta-data/)

```sh
$ curl http://169.254.169.254/latest/dynamic/instance-identity/document
{
  "accountId" : "561279834",
  "architecture" : "x86_64",
  "availabilityZone" : "us-east-1e",
  "billingProducts" : null,
  "devpayProductCodes" : null,
  "marketplaceProductCodes" : null,
  "imageId" : "ami-09d95fab7fff3776c",
  "instanceId" : "i-04031fa4bbfc30d87",
  "instanceType" : "t2.micro",
  "kernelId" : null,
  "pendingTime" : "2020-06-18T10:10:57Z",
  "privateIp" : "172.31.54.69",
  "ramdiskId" : null,
  "region" : "us-east-1",
  "version" : "2017-09-30"
}
```

#### Usage
```sh
python metadata.py
```
* it is avoided to use any dependencies.

#### output
```sh
DEVPAY_PRODUCT_CODES=None
AVAILABILITY_ZONE=us-east-1e
INSTANCE_ID=i-04031fa4bbfc30d87
PENDING_TIME=2020-06-18T10:10:57Z
MARKETPLACE_PRODUCT_CODES=None
REGION=us-east-1
IMAGE_ID=ami-09d95fab7fff3776c
VERSION=2017-09-30
ARCHITECTURE=x86_64
BILLING_PRODUCTS=None
KERNEL_ID=None
RAMDISK_ID=None
PRIVATE_IP=172.31.54.69
INSTANCE_TYPE=t2.micro
ACCOUNT_ID=561279834
```

## Using ec2-metadaa cmd
on ec2 you can run `ec2-metadata` command to retrieve get metadata for specific key.

```sh
ec2-metadata v0.1.2
Use to retrieve EC2 instance metadata from within a running EC2 instance. 
e.g. to retrieve instance id: ec2-metadata -i
 to retrieve ami id: ec2-metadata -a
 to get help: ec2-metadata --help
For more information on Amazon EC2 instance meta-data, refer to the documentation at
http://docs.amazonwebservices.com/AWSEC2/2008-05-05/DeveloperGuide/AESDG-chapter-instancedata.html

Usage: ec2-metadata <option>
Options:
--all                     Show all metadata information for this host (also default).
-a/--ami-id               The AMI ID used to launch this instance
-l/--ami-launch-index     The index of this instance in the reservation (per AMI).
-m/--ami-manifest-path    The manifest path of the AMI with which the instance was launched.
-n/--ancestor-ami-ids     The AMI IDs of any instances that were rebundled to create this AMI.
-b/--block-device-mapping Defines native device names to use when exposing virtual devices.
-i/--instance-id          The ID of this instance
-t/--instance-type        The type of instance to launch. For more information, see Instance Types.
-h/--local-hostname       The local hostname of the instance.
-o/--local-ipv4           Public IP address if launched with direct addressing; private IP address if launched with public addressing.
-k/--kernel-id            The ID of the kernel launched with this instance, if applicable.
-z/--availability-zone    The availability zone in which the instance launched. Same as placement
-c/--product-codes        Product codes associated with this instance.
-p/--public-hostname      The public hostname of the instance.
-v/--public-ipv4          NATted public IP Address
-u/--public-keys          Public keys. Only available if supplied at instance launch time
-r/--ramdisk-id           The ID of the RAM disk launched with this instance, if applicable.
-e/--reservation-id       ID of the reservation.
-s/--security-groups      Names of the security groups the instance is launched in. Only available if supplied at instance launch time
-d/--user-data            User-supplied data.Only available if supplied at instance launch time.
```
