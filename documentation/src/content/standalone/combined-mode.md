---
title: Combined Mode
weight: 4
---

Combined Mode allows for both HTTP Mode and OpenTelemetry mode metrics collections methods.

### HTTP Mode

Exposes metric using an HTTP endpoint.

- metrics are collected when the HTTP endpoint is accessed
- "pull" model

### OpenTelemtry Mode

Pushes metrics to an OpenTelemetry endpoint.

- metrics are periodically collected and pushed OpenTelemetry endpoint
- "push" model

# Installation

### Example

```shell
java -jar jmx_prometheus_standalone-<VERSION>.jar [HOSTNAME:]<PORT> <EXPORTER.YAML>
```

**NOTES**

- `<PORT>` is required
- `[HOSTNAME]` is optional

### Concrete Example

```shell
java -jar jmx_prometheus_standalone-1.1.0.jar 12345 exporter.yaml
```

# Basic YAML Configuration

**exporter.yaml**

```yaml
openTelemetry:
  endpoint: http://prometheus:9090/api/v1/otlp
  protocol: http/protobuf
  interval: 60
rules:
- pattern: ".*"
```

# Advanced YAML Configuration

Reference HTTP Mode [Rules](/rules/rules/) for various `exporter.yaml` metrics configuration options.

# Metrics

1. Run your application.
2. Access HTTP Mode metrics using a browser to view your metrics.

```
http://<APPLICATION_HOSTNAME>:<PORT>/metrics
```

```
# HELP my_count_total example counter
# TYPE my_count_total counter
my_count_total{status="error"} 1.0
my_count_total{status="ok"} 2.0
```

3. Access your OpenTelemetry platform to view OpenTelemetry metrics.