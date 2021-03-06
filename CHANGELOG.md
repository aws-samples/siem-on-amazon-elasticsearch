# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.3.0] - 2021-03-20
### Added
- Supported and normalized log: AWS Network Firewall, Amazon MSK(Blokder log), Amazon RDS(MariaDB/MySQL/PostgreSQL), vpc flow logs v5 format #5,#6,#17,#62,#67,#71
- Added multiline-text log parser #54
- Enabled system log of Amazon ES instance during initial deployment #64
- Enabled parsing china region and Gov Cloud for CloudTrail #72

### Changed
- Refactored deployment script with crhelper #69
- Changed frequency of updating GeoDB from 0:20UTC to every 12 hours #70
- Changed s3_key of s3access log to regex. Users don't need to change anything #74

### Fixed
- Fixed parse issue: responseElements.credentials, requestParameters.CreateSnapshotsRequest.TagSpecification.Tag.Value, requestParameters.source, responseElements.multiAZ, requestParameters.partitionInputList, responseElements.errors.partitionValues of CloudTrail #33,#59,#66,#67,#75,#76
- Fixed issue with importing no data log #53
- Followed ECS rule for dns.question.name of vpc dns query log #60
- Fixed extracting distribution_id of CloudFront #61
- Fixed ambiguous error message like "[[], [], [], [], []]" may appear #68
- fixed ECS violation field, event.severity of Security Hub #77

### Security
- PR security vulnerability of urllib3 from 1.26.2 to 1.26.3 #78,#79

## [2.2.0] - 2021-02-07
### Added
- Added IAM role for EC2 to import ETL existing Logs in S3 #41
- Supported timestamp with nested field #38
- Added custom metrics of es-loader for CloudWatch Metrics #13
- Enabled memory caching of Lambda function, es-loader. When hitting cache, parsing will be 500x faster. Other logics are also tuned up #39,#45

### Changed
- Changing plain logging to structured logging of es-loader #13
- Allowed Amazon Athena to query S3 bucket made by SIEM #35
- Changed S3 file path of CloudFormation template. This affect only when you create own CloudFormation template #51
- Changed default Amazon ES's system index setting such as .opendistro-alerting-alert-history #48
- Limited number of es-loader's concurrency to avoid abnormal situation. Default is 10. You can change it to input CloudFormation parameter #43

### Deprecaed
- Helper functions in siem class such as merge function. Re-wrote and moved to siem.utils.py #39, #45

### Removed
- Removed legacy parsing timestamp code. It used until v1.5.2
- Removed feature of importing logs from Kinesis Data Stream

### Fixed
- Fixed SQS timeout issue in VPC #52
- Fixed parse issue, ELB logs with space(#50, #47), CloudFront Logs with IPv6(#46), non-ascii and JSON logs(#49)
- Fixed NuSuchKey error when S3 key includes meta character #42

## [2.1.1] - 2020-12-28
### Added
- Deep Security Support #27

### Fixed
- Parse issue of S3 access logs with double quotes on the UA. #34
- Parse issue of  ALB and CLB logs when IPv6 address is contained #31
- Issue with key policy created by CDK #32
- VPC config validation raises KeyError when using VPC peering instead IGW #29

## [2.1.0] - 2020-12-14
### Added
- Supported and normalized log: Security Hub(Security Hub, GuardDuty, Macie, IAM Analyzer, Inspector), Linux SSH log via CWL, ECS via Firelens(Framework only) #7
- Dashboard: ELB, Security Hub(GuardDuty) #1,#18
- Split and parse logs in parallel when logs are huge.
- Functionality of filtering unnecessary logs #19
- Supported nano seconds of es-loader(just truncated) #23

### Changed
- Amazon ES's initial version to v7.9.1 from v7.7.0 #24
- Increased es-loader's memory to 2048 MB from 512 MB #21
- Fix version in deployment procedure: Node(Active LTS), Python(3.8) #25,#26
- Dashboard: changed findings count logic of GuardDuty #20
- Enhanced extract logic of AWS account and region

### Fixed
- An error occurred when processing the file of size 0 byte with es-loader #15
- CLB logs parsing fails #16
- Regex error of S3 access log and CloudFront
- Typo of GuardDuty dashboard

## [2.0.0] - 2020-10-23
### Added
- All files, initial version
