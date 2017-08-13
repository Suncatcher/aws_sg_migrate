aws_sg_migrate.py
=====================
Python3 script for migrating AWS EC2 Security Groups across availability regions

## Initial configuration
One should have Python3 and Bash and AWS CLI properly installed. No special ocnfiguration is needed.
AWS Access Key and Secret Key are taken from default profile (`~/.aws`). They can be set by `aws configure`.

## Initial script parameters

* --h (help) <br>
Shows available keys and their behavior
* --s (help) <br>
Wraps AWS CLI commands into Shell
* --v (vpc) <br>
Sets VPC ID of destination VPC
* --sc (source) <br>
Sets source AWS availability region
* --ds (dest) <br>
Sets detination AWS availability region
* Security Group ID
Non-prefix parameter, denoting which group is to be migrated.

## Usage
The solution consists of two scripts: initial generation Pyhton script and resulting Bash script for creating Security Groups.
With the first script user sets desired parameters, from wich intermediate Bash scripts with AWS CLI command is generated.
For creating Security Groups one should run this Bash script.

The initial script runs as following:

	python3 aws_sg_migrate.py --vpc=vpc-05643b6c --shell --source=us-east-1 --dest=us-west-1 sg-74323418

### More usage examples:
For creating pure AWS CLI commands

	python3 aws_sg_migrate.py --vpc=vpc-05643b6c --source=us-east-1 --dest=us-west-1 sg-74323418
  
For migrating Security Groups from current region `--source` parameter can be omitted. The current region is taken from profile

	python3 aws_sg_migrate.py --vpc=vpc-05643b6c --source=us-east-1 --dest=us-west-1 sg-74323418

