# intro-to-terraform-and-ansible

A hands-on workshop to become familiar with [Hashicorp Terraform](https://www.terraform.io/)
to provision and configure infrastructure and [Red Hat Ansible](https://github.com/ansible/ansible)
to configure systems and deploy applications.

## Lessons

### Terraform lessons

* [Lesson-01](lesson-01/README.md) - Terraform basics
* [Lesson-02](lesson-02/README.md) - Terraform variables, output, and data
* [Lesson-03](lesson-03/README.md) - More Terraform variables, plans, workspaces, and security
* [Lesson-04](lesson-04/README.md) - Building an Ansible sandbox

### Ansible lessons

* [Lesson-05](lesson-05/README.md) - Ansible basics
* [Lesson-06](lesson-06/README.md) - Playbook basics
* [Lesson-07](lesson-07/README.md) - Practical Ansible
* [Lesson-08](lesson-08/README.md) - Full web application

### Demo

* [Demo-09](demo-09/README.md) - Putting it all together

## Reference documentation

* [Terraform AWS provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
* [Ansible built-in plugins](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/)

## Prerequisites

To get the most out of this workshop, you will need the following:

* Terraform installed
* SSH client
* AWS account with adequate permissions
* AWS CLI installed and configured
* AWS EC2 key pair

### Terraform

[Install Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started)
on your laptop and make sure it is on your path.

```console
$ terraform --version
Terraform v1.1.9
on linux_amd64
```

### SSH client

You should have an SSH client installed and be familiar with using it.
[PuTTY](https://www.putty.org/) is an option for Windows, but most Windows users
will be better served with the client that comes with [Git Bash](https://gitforwindows.org/).
Other OSes likely have the client already installed.

```console
$ ssh -V
OpenSSH_8.9p1, OpenSSL 1.1.1n  15 Mar 2022
```

### AWS account with adequate permissions

You'll need an AWS account. The [AWS Free Tier](https://aws.amazon.com/free/)
is sufficient.

If you are not the root account holder, make sure you have sufficient permissions
to create EC2 instances. The AWS Managed `AmazonEC2FullAccess` policy should be
enough.

You will need an `AWS Access Key ID` and `AWS Secret Access Key` available to you.
[Creating an access key](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)
specifically for this workshop might be a good idea.

### AWS CLI installed and configured

You must install the [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
and configure it to use the `AWS Access Key ID` and `AWS Secret Access Key` you
created previously.

Use `aws configure` to [set up](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html)
the AWS CLI to use them.

Ensure the configuration is in place and you can access AWS via the CLI.

```console
$ aws configure
AWS Access Key ID [****************5X4R]:
AWS Secret Access Key [****************ojQ8]:
Default region name [us-east-2]:
Default output format [json]:
$ aws sts get-caller-identity
{
    "UserId": "AIDAQZROKXPRRMDCYPJNQ",
    "Account": "054858005475",
    "Arn": "arn:aws:iam::054858005475:user/gene.gotimer-terraform"
}
```

### AWS EC2 key pair

[Create an EC2 key pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair)
and configure your SSH client to use it. Some clients (*cough* PuTTY *cough*)
need the key converted for use, so pay attention to your SSH client documentation.

```console
$ aws ec2 describe-key-pairs
{
    "KeyPairs": [
        {
            "KeyPairId": "key-0a0b1b7ec358fca13",
            "KeyFingerprint": "41:ae:37:68:64:18:24:4b:be:46:77:93:d8:b0:51:07:90:d1:29:8b",
            "KeyName": "gene-test-us-east-2",
            "Tags": []
        }
    ]
}
```

We will be copying the public **and private** keys on to AWS EC2 instances, so you
might want to create a key pair just for this workshop and then delete it immediately
after, just in case.
