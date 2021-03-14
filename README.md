<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/tag-reporter/blob/master/README.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# Lambda Function CloudFormation Blueprint

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

![CodeBuild](https://codebuild.us-west-2.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiK0xUWGozRzNyWUFTemZQcEVMb3k5ckZMR3NIMVhHSGJrcVBBRVROY3FMWS91Z0paZDdJN215VDkrWXRaM3R0dGtVT3lXRFc3Tm1hVFloS2ZqekZVRk9nPSIsIml2UGFyYW1ldGVyU3BlYyI6IkdBbEtRNkJ6Rzd2ZXBvZ0QiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=master)

This blueprint provisions a [ConfigRule](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html) 
to check AWS resources for the presence of required tags and an associated [Lambda Function](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-lambda-function.html)
that checks if resources comply with the rule on a regular (1 hour) interval.

* A list of required tags is [configurable](#configure) and defaults to ["Backup", "Owner"]
* A list of AWS resource types to check is [configurable](#configure) and defaults to ["AWS::EC2::Instance","AWS::EC2::Volume"]

## Usage

1. Add blueprint to Gemfile
2. Configure: configs/tag-reporter values
3. Deploy blueprint

## Add

Add the blueprint to your lono project's `Gemfile`.

```ruby
gem "tag-reporter", git: "git@github.com:boltopspro/tag-reporter.git"
```

## Configure
 
Use the [lono seed](https://lono.cloud/reference/lono-seed/) command to generate a starter config params files.

    LONO_ENV=development lono seed tag-reporter
    LONO_ENV=production  lono seed tag-reporter

The files in `config/tag-reporter` folder will look something like this:

    configs/tag-reporter/
    └── variables
        ├── development.rb
        └── production.rb

Configure the `configs/tag-reporter/variables` files.

Use **@required_tags** to specify tag names to check for.

Use **@resource_types** to specify AWS resource types to check. Currently supported types are "AWS::EC2::Instance" and "AWS::EC2::Volume"

## Deploy

Use the [lono cfn deploy](http://lono.cloud/reference/lono-cfn-deploy/) command to deploy.

    LONO_ENV=development lono cfn deploy tag-reporter --sure --no-wait
    LONO_ENV=production  lono cfn deploy tag-reporter --sure --no-wait

If you are using One AWS Account, use these commands instead: [One Account](docs/one-account.md).