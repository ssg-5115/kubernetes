apiVersion: v1
kind: Namespace
metadata:
  name: my-custom-namespace
  labels:
    environment: production
    team: backend
  annotations:
    owner: devops-team@example.com
    purpose: "Isolated namespace for backend services"
