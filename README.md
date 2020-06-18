## Retrieving EC2 instance metadata to import to systemd

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

### Usage
```sh
python metadata.py
```
* it is avoided to use any dependencies.

### output
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
