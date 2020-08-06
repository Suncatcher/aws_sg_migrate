aws_sg_migrate.py
=====================
Python3 script for migrating AWS EC2 Security Groups across availability regions

## Initial configuration
One should have Python3 and Bash and AWS CLI properly installed. No special configuration is needed.<br>
AWS Access Key and Secret Key are taken from default profile (`~/.aws`). They can be set by `aws configure`.

## Initial script parameters

`--h (help)` <br>
Shows available keys and their behavior <br>
`--s (shell)` <br>
Wraps AWS CLI commands into Shell. Optional. <br>
`--v (vpc)` <br>
Sets VPC ID of destination VPC. Optional. <br>
`--sc (src)` <br>
Sets source AWS availability region <br>
`--ds (dest)` <br>
Sets destination AWS availability region. Optional.<br>
`Security Group ID` <br>
Non-prefix parameter, denoting which group is to be migrated

## Usage
The solution consists of two scripts: initial generation Pyhton script and resulting Bash script for creating Security Groups.
With the first script user sets desired parameters, from wich intermediate Bash scripts with AWS CLI commands is generated. For creating Security Groups one should run this generated Bash script. In case group with the same name is found in destination region it is recreated with the updated rules.

The initial script runs as following:

	python3 aws_sg_migrate.py --vpc=vpc-05643b6c --shell --src=us-east-1 --dest=us-west-1 sg-74323418

### More usage examples:
For creating pure AWS CLI commands

	python3 aws_sg_migrate.py --vpc=vpc-05643b6c --src=us-east-1 --dest=us-west-1 sg-74323418
  
For migrating Security Groups from current region `--src` parameter can be omitted. The current region is taken from profile

	python3 aws_sg_migrate.py --vpc=vpc-05643b6c --src=us-east-1 --dest=us-west-1 sg-74323418
	
For replicating single Security Group into all regional availability zones `--vpc` parameter can be omitted. In this case all VPC IDs are taken from the dictionary in the begginning of the script.

	python3 aws_sg_migrate.py --src=us-east-1 sg-74323418

