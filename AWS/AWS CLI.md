# AWS CLI

## Links
- [AWS All Docs](https://docs.aws.amazon.com/)
- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html)
- [AWS CLI Configuration and Credential File Settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
- [AWS CLI Command Reference](https://docs.aws.amazon.com/cli/latest/index.html)
- [AWS CLI Reference Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-help.html#cli-reference)

## Where to run
- Linux shells – Use common shell programs such as bash, zsh, and tcsh to run commands in Linux or macOS.
- Windows command line – On Windows, run commands at the Windows command prompt or in PowerShell.
- Remotely – Run commands on Amazon Elastic Compute Cloud (Amazon EC2) instances through a remote terminal program such as PuTTY or SSH, or with AWS Systems Manager.

## AWS CLI Get Help
- [AWS CLI Get Help](https://docs.aws.amazon.com/cli/latest/userguide/cli-getting-help.html)
```shell
aws help
# or
aws <command> help
```

## AWS CLI Command Structure
- [AWS CLI Command Structure](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-commandstructure.html)

1. The base call to the aws program.
2. The top-level command, which typically corresponds to an AWS service supported by the AWS CLI.
3. The subcommand that specifies which operation to perform.
4. General AWS CLI options or parameters required by the operation. You can specify these in any order as long as they follow the first three parts. If an exclusive parameter is specified multiple times, only the last value applies.
```shell
aws <command> <subcommand> [options and parameters]
```
## AWS CLI Configuration and Credential File Settings
- [AWS CLI Configuration and Credential File Settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html)
- [Specifying a profile to use](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
- [Configuring the AWS CLI to use AWS Single Sign-On](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html)

You can keep all of your profile settings in a single file as the AWS CLI can read credentials from the config file. If there are credentials in both files for a profile sharing the same name, the keys in the credentials file take precedence. We suggest keeping credentials in the credentials files. These files are also used by the various language software development kits (SDKs). If you use one of the SDKs in addition to the AWS CLI, confirm if the credentials should be stored in their own file.

### Custom Config Locations
- [Customizing CLI Configs and Credential File](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)
By default, the AWS CLI stores the config and credential files in the .aws subdirectory of your home directory:
- Linux and macOS: ~/.aws/
- Windows: C:\Users\<YourUsername>\.aws\
%UserProfile% in Windows and $HOME or ~ (tilde) in Unix-based systems. You can specify a non-default location for the files by setting the AWS_CONFIG_FILE and AWS_SHARED_CREDENTIALS_FILE environment variables to another local path

### Lots more config options, check the docs

## Configuring CLI Environment Variables
- [Configuring the AWS CLI Environment Variables](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)
- [AWS CLI Environment Variables Reference](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html#envvars-reference)

## AWS CLI Options
- [AWS Command Line Options](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-options.html)
- [AWS CLI Command Options](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-options.html)
- [Common AWS CLI Options](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-options.html#common-options)
```shell
--color
--debug
--endpoint-url <string>
# output has lots of options
--output <string>
    # json | yaml | yaml-stream | table | text | csv
--query <string>
# ...etc
```
### --output
The --output option specifies the formatting style for command output. The available output formats are:
- [json](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#json-output) – The output is formatted as a JSON string. This is the default format.
- [yaml](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#yaml-output) – The output is formatted as a YAML string.
- [yaml-stream](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#yaml-stream-output) – The output is formatted as a stream of YAML documents.
- [table](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#table-output) – The output is formatted as a table.
- [text](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#text-output) – The output is formatted as plain text.
- [csv](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#csv-output) – The output is formatted as comma-separated values.

### --query 
The --query option uses JMESPath syntax to filter the output of AWS CLI commands. JMESPath is a query language for JSON that allows you to extract and transform elements from a JSON document.
- [JMESPath Tutorial](https://jmespath.org/tutorial.html)
- [JMESPath Specification](https://jmespath.org/specification.html)
```shell
$ aws ec2 describe-instances --output table --region us-west-1
-------------------
|DescribeInstances|
+-----------------+
$ aws ec2 describe-instances --output table --region us-west-2
------------------------------------------------------------------------------
|                              DescribeInstances                             |
+----------------------------------------------------------------------------+
||                               Reservations                               ||
|+-------------------------------------+------------------------------------+|
||  OwnerId                            |  012345678901                      ||
||  ReservationId                      |  r-abcdefgh                        ||
|+-------------------------------------+------------------------------------+|
|||                                Instances                               |||
||+------------------------+-----------------------------------------------+||
|||  AmiLaunchIndex        |  0                                            |||
|||  Architecture          |  x86_64                                       |||
```

## AWS CLI Endpoints
- [AWS CLI Endpoints](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-endpoints.html)
- [Set a single endpoint for a single command](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-endpoints.html#endpoints-command)
- [Set a single endpoint for all commands for a specific service](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-endpoints.html#endpoints-service)
- [Set a single endpoint for all commands for all services](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-endpoints.html#endpoints-all)
- [Endpoint Configuration and Settings](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-endpoints.html#endpoints-precedence)

## AWS Output Formatting
- [AWS CLI Output Formatting](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output.html)
- [AWS CLI Output Formatting Examples](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-examples.html)
- [AWS CLI Output Formatting Reference](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html)

```shell
aws s3api list-buckets --query "Buckets[].Name"
[
    "example-bucket-1",
    "example-bucket-2",
    "example-bucket-3"
]
```
```shell
aws iam list-users --output yaml-stream
- IsTruncated: false
  Users:
  - Arn: arn:aws:iam::123456789012:user/Admin
    CreateDate: '2014-10-16T16:03:09+00:00'
    PasswordLastUsed: '2016-06-03T18:37:29+00:00'
    Path: /
    UserId: AIDA1111111111EXAMPLE
    UserName: Admin
  - Arn: arn:aws:iam::123456789012:user/backup/backup-user
    CreateDate: '2019-09-17T19:30:40+00:00'
    Path: /backup/
    UserId: AIDA2222222222EXAMPLE
    UserName: arq-45EFD6D1-CE56-459B-B39F-F9C1F78FBE19
  - Arn: arn:aws:iam::123456789012:user/cli-user
    CreateDate: '2019-09-17T19:30:40+00:00'
    Path: /
    UserId: AIDA3333333333EXAMPLE
    UserName: cli-user
```

## AWS CLI Return Codes
- [AWS CLI Return Codes](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-returncodes.html)
- [AWS CLI Common Return Codes](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-return-codes.html#common-return-codes)

Code	Meaning
- `0`	- The service responded with an HTTP response status code of 200 indicating that there were no errors generated by the AWS CLI and AWS service the request was sent to.
- `1`	- One or more Amazon S3 transfer operations failed. Limited to S3 commands.
- `2`	- The meaning of this return code depends on the command:
  - Applicable to all AWS CLI commands – the command entered couldn't be parsed. Parsing failures can be caused by, but aren't limited to, missing required subcommands or arguments, or using unknown commands or arguments.
  - Limited to S3 commands – One or more files marked for transfer were skipped during the transfer process. However, all other files marked for transfer were successfully transferred. Files that are skipped during the transfer process include: files that don't exist; files that are character special devices, block special device, FIFO queues, or sockets; and files that the user doesn't have read permissions to.
- `130` - The command was interrupted by a SIGINT. This is the signal sent by you to cancel a command with Ctrl+C.
- `252` - Command syntax was invalid, an unknown parameter was provided, or a parameter value was incorrect and prevented the command from running.
- `253` - The system environment or configuration was invalid. While the command provided might be syntactically valid, missing configuration or credentials prevented the command from running.
- `254` - The command successfully parsed and a request made to the specified service but the service returned an error. This will generally indicate incorrect API usage or other service specific issues.
- `255` - The command failed. There were errors generated by the AWS CLI or by the AWS service to which the request was sent.