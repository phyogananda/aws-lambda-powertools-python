# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.7.0] - 2020-10-26

### Added
- **Utilities**: Add new `Parser` utility to provide parsing and deep data validation using Pydantic Models
- **Utilities**: Add case insensitive header lookup, and Cognito custom auth triggers to `Event source data classes`

### Fixed
- **Logger**: keeps Lambda root logger handler, and add log filter instead to prevent child log records duplication
- **Docs**: Improve wording on adding log keys conditionally

## [1.6.1] - 2020-09-23

### Fixed
- **Utilities**: Fix issue with boolean values in DynamoDB stream event data class.

## [1.6.0] - 2020-09-22

### Added
- **Metrics**: Support adding multiple metric values to a single metric name
- **Utilities**: Add new `Validator` utility to validate inbound events and responses using JSON Schema
- **Utilities**: Add new `Event source data classes` utility to easily describe event schema of popular event sources
- **Docs**: Add new `Testing your code` section to both Logger and Metrics page, and content width is now wider
- **Tracer**: Support for automatically disable Tracer when running a Chalice app

### Fixed
- **Docs**: Improve wording on log sampling feature in Logger, and removed duplicate content on main page
- **Utilities**: Remove DeleteMessageBatch API call when there are no messages to delete

## [1.5.0] - 2020-09-04

### Added
- **Logger**: Add `xray_trace_id` to log output to improve integration with CloudWatch Service Lens
- **Logger**: Allow reordering of logged output
- **Utilities**: Add new `SQS batch processing` utility to handle partial failures in processing message batches
- **Utilities**: Add typing utility providing static type for lambda context object
- **Utilities**: Add `transform=auto` in parameters utility to deserialize parameter values based on the key name

### Fixed
- **Logger**: The value of `json_default` formatter is no longer written to logs

## [1.4.0] - 2020-08-25

### Added
- **All**: Official Lambda Layer via [Serverless Application Repository](https://serverlessrepo.aws.amazon.com/applications/eu-west-1/057560766410/aws-lambda-powertools-python-layer)
- **Tracer**: `capture_method` and `capture_lambda_handler` now support **capture_response=False** parameter to prevent Tracer to capture response as metadata to allow customers running Tracer with sensitive workloads

### Fixed
- **Metrics**: Cold start metric is now completely separate from application metrics dimensions, making it easier and cheaper to visualize.
    - This is a breaking change if you were graphing/alerting on both application metrics with the same name to compensate this previous malfunctioning
    - Marked as bugfix as this is the intended behaviour since the beginning, as you shouldn't have the same application metric with different dimensions
- **Utilities**: SSMProvider within Parameters utility now have decrypt and recursive parameters correctly defined to support autocompletion

### Added
- **Tracer**: capture_lambda_handler and capture_method decorators now support `capture_response` parameter to not include function's response as part of tracing metadata

## [1.3.1] - 2020-08-22
### Fixed
- **Tracer**: capture_method decorator did not properly handle nested context managers

## [1.3.0] - 2020-08-21
### Added
- **Utilities**: Add new `parameters` utility to retrieve a single or multiple parameters from SSM Parameter Store, Secrets Manager, DynamoDB, or your very own

## [1.2.0] - 2020-08-20
### Added
- **Tracer**: capture_method decorator now supports generator functions (including context managers)

## [1.1.3] - 2020-08-18
### Fixed
- **Logger**: Logs emitted twice, structured and unstructured, due to Lambda configuring the root handler

## [1.1.2] - 2020-08-16
### Fixed
- **Docs**: Clarify confusion on Tracer reuse and `auto_patch=False` statement
- **Logger**: Autocomplete for log statements in PyCharm

## [1.1.1] - 2020-08-14
### Fixed
- **Logger**: Regression on `Logger` level not accepting `int` i.e. `Logger(level=logging.INFO)`

## [1.1.0] - 2020-08-14
### Added
- **Logger**: Support for logger inheritance with `child` parameter

### Fixed
- **Logger**: Log level is now case insensitive via params and env var

## [1.0.2] - 2020-07-16
### Fixed
- **Tracer**: Correct AWS X-Ray SDK dependency to support 2.5.0 and higher

## [1.0.1] - 2020-07-06
### Fixed
- **Logger**: Fix a bug with `inject_lambda_context` causing existing Logger keys to be overridden if `structure_logs` was called before

## [1.0.0] - 2020-06-18
### Added
- **Metrics**: `add_metadata` method to add any metric metadata you'd like to ease finding metric related data via CloudWatch Logs
- Set status as General Availability

## [0.11.0] - 2020-06-08
### Added
- Imports can now be made from top level of module, e.g.: `from aws_lambda_powertools import Logger, Metrics, Tracer`

### Fixed
- **Metrics**: Fix a bug with Metrics causing an exception to be thrown when logging metrics if dimensions were not explicitly added.

### Changed
- **Metrics**: No longer throws exception by default in case no metrics are emitted when using the log_metrics decorator.

## [0.10.0] - 2020-06-08
### Added
- **Metrics**: `capture_cold_start_metric` parameter added to `log_metrics` decorator
- **Metrics**: Optional `namespace` and `service` parameters added to Metrics constructor to more closely resemble other core utils

### Changed
- **Metrics**: Default dimension is now created based on `service` parameter or `POWERTOOLS_SERVICE_NAME` env var

### Deprecated
- **Metrics**: `add_namespace` method deprecated in favor of using `namespace` parameter to Metrics constructor or `POWERTOOLS_METRICS_NAMESPACE` env var

## [0.9.5] - 2020-06-02
### Fixed
- **Metrics**: Coerce non-string dimension values to string
- **Logger**: Correct `cold_start`, `function_memory_size` values from string to bool and int respectively

## [0.9.4] - 2020-05-29
### Fixed
- **Metrics**: Fix issue where metrics were not correctly flushed, and cleared on every invocation

## [0.9.3] - 2020-05-16
### Fixed
- **Tracer**: Fix Runtime Error for nested sync due to incorrect loop usage

## [0.9.2] - 2020-05-14
### Fixed
- **Tracer**: Import aiohttp lazily so it's not a hard dependency

## [0.9.0] - 2020-05-12
### Added
- **Tracer**: Support for async functions in `Tracer` via `capture_method` decorator
- **Tracer**: Support for `aiohttp` via `aiohttp_trace_config` trace config
- **Tracer**: Support for patching specific modules via `patch_modules` param
- **Tracer**: Document escape hatch mechanisms via `tracer.provider`

## [0.8.1] - 2020-05-1
### Fixed
* **Metrics**: Fix metric unit casting logic if one passes plain string (value or key)
* **Metrics:**: Fix `MetricUnit` enum values for
    - `BytesPerSecond`
    - `KilobytesPerSecond`
    - `MegabytesPerSecond`
    - `GigabytesPerSecond`
    - `TerabytesPerSecond`
    - `BitsPerSecond`
    - `KilobitsPerSecond`
    - `MegabitsPerSecond`
    - `GigabitsPerSecond`
    - `TerabitsPerSecond`
    - `CountPerSecond`

## [0.8.0] - 2020-04-24
### Added
- **Logger**: Introduced `Logger` class for structured logging as a replacement for `logger_setup`
- **Logger**: Introduced `Logger.inject_lambda_context` decorator as a replacement for `logger_inject_lambda_context`

### Removed
- **Logger**: Raise `DeprecationWarning` exception for both `logger_setup`, `logger_inject_lambda_context`

## [0.7.0] - 2020-04-20
### Added
- **Middleware factory**: Introduced Middleware Factory to build your own middleware via `lambda_handler_decorator`

### Fixed
- **Metrics**: Fixed metrics dimensions not being included correctly in EMF

## [0.6.3] - 2020-04-09
### Fixed
- **Logger**: Fix `log_metrics` decorator logic not calling the decorated function, and exception handling

## [0.6.1] - 2020-04-08
### Added
- **Metrics**: Introduces Metrics middleware to utilise CloudWatch Embedded Metric Format

### Deprecated
- **Metrics**: Added deprecation warning for `log_metrics`

## [0.5.0] - 2020-02-20
### Added
- **Logger**: Introduced log sampling for debug - Thanks to [Danilo's contribution](https://github.com/awslabs/aws-lambda-powertools/pull/7)

## [0.1.0] - 2019-11-15
### Added
- Public beta release
