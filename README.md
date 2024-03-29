# fluent-bit-multiline
Fast and Lightweight Logs and Metrics processor for Linux, BSD, OSX and Windows.

The main goal of this project is to extend the default aws-for-fluent-bit docker image
to support `partial_message` mode of fluent bit. Partial/Split container logs are then concatenated into one log.
This is useful if the logging destination expects logs to be single line or if you 
log in JSON format (for ex. to Datadog or OpenSearch).

For more information, see here: [Example from AWS](https://github.com/aws-samples/amazon-ecs-firelens-examples/tree/mainline/examples/fluent-bit/filter-multiline-partial-message-mode)

The config also configures the container to provide an endpoint for healthcheck data.
Go to the [FluentBit Documentation](https://docs.fluentbit.io/manual/administration/monitoring#health-check-for-fluent-bit) for more information.

## Usage

Use this image inside of container definitions for AWS ECS Services. Make sure to reference the custom configuration
file! Example:

```json
{
  "image": "ghcr.io/hapag-lloyd/fluent-bit-multiline:edge",
  "name": "log_router",
  "memoryReservation": 50,
  "firelensConfiguration": {
    "type": "fluentbit",
    "options": {
      "config-file-type": "file",
      "config-file-value": "/extra.conf"
    }
  }
}
```
