kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/latest/download/opentelemetry-operator.yaml


kubectl get pods -n opentelemetry-operator-system

apiVersion: opentelemetry.io/v1alpha1
kind: OpenTelemetryCollector
metadata:
  name: otel-collector
  namespace: observability
spec:
  mode: deployment
  config: |
    receivers:
      otlp:
        protocols:
          grpc:
          http

    processors:
      batch:

    exporters:
      logging:
        loglevel: debug

    service:
      pipelines:
        traces:
          receivers: [otlp]
          processors: [batch]
          exporters: [logging]
        metrics:
          receivers: [otlp]
          processors: [batch]
          exporters: [logging]
        logs:
          receivers: [otlp]
          processors: [batch]
          exporters: [logging]


kubectl apply -f otel-collector.yaml


kubectl get pods -n observability
kubectl logs -n observability deployment/otel-collector

    
