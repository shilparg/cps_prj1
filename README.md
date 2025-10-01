# cps_prj1

```markdown
# Intelligent IoT Integration Pipeline with AWS

## Overview

This capstone project demonstrates a secure, event-driven IoT architecture using AWS services. It integrates BLE and Modbus telemetry from commercial sensors into AWS IoT Core, routes data through a cloud-native pipeline, and applies machine learning for real-time anomaly detection. The infrastructure is defined using Terraform and aligned with NIST cybersecurity principles and ISO 26262 safety lifecycle goals.

---

## Architecture Summary

**Edge Layer**
- BLE sensor (commercial device) sends telemetry via BLE to gateway
- Modbus sensor polled by Raspberry Pi using Modbus RTU/TCP
- Gateway publishes JSON payloads to AWS IoT Core via MQTT

**AWS Cloud Pipeline**
- **AWS IoT Core**: Ingests MQTT messages
- **IoT Rules Engine**: Routes data to:
  - **Amazon SQS**: Buffering
  - **AWS Lambda**: Transformation and validation
  - **Amazon SNS**: Alerting
  - **Amazon DynamoDB / S3**: Storage

**ML/AI Layer**
- **Amazon SageMaker**: Trains and hosts anomaly detection models
- **Lambda**: Invokes SageMaker endpoint for real-time inference
- **S3 / SageMaker Pipelines**: Stores data and automates retraining

**Security & Compliance**
- IAM Access Analyzer for least privilege
- GuardDuty and Macie for threat detection and data sensitivity
- CloudTrail for audit logging
- Terraform for infrastructure-as-code and reproducibility

---

## Technologies Used

| Domain            | Tools & Services                          |
|------------------|-------------------------------------------|
| IoT Ingestion     | BLE, Modbus RTU/TCP, MQTT, AWS IoT Core   |
| Event Processing  | Lambda, SQS, SNS, DynamoDB, S3            |
| ML/AI             | SageMaker, SageMaker Pipelines, CloudWatch|
| Security & Audit  | IAM, GuardDuty, Macie, CloudTrail         |
| Infrastructure    | Terraform                                 |

---

## Repository Structure

```
├── terraform/
│   ├── iot-core.tf
│   ├── lambda.tf
│   ├── sagemaker.tf
│   ├── iam.tf
│   └── outputs.tf
├── lambda/
│   └── invoke_model.py
├── data/
│   └── sample_sensor_data.json
├── README.md
```

---

## Sample Workflow

1. BLE and Modbus sensors send telemetry to gateway
2. Gateway publishes data to AWS IoT Core via MQTT
3. IoT Rule triggers Lambda → invokes SageMaker model
4. Prediction routed to SNS (alert) and DynamoDB (logging)
5. CloudTrail logs activity; GuardDuty monitors threats
6. Terraform provisions all resources with audit-ready tags

---

## ML Model Details

- Algorithm: XGBoost (for anomaly detection)
- Input: Temperature, humidity, vibration
- Output: Anomaly score or classification
- Retraining: Automated via SageMaker Pipelines

---

## Compliance Alignment

- **NIST Cybersecurity Framework**  
  Identify → Protect → Detect → Respond → Recover

- **ISO 26262 Safety Lifecycle**  
  Fault injection, diagnostics, traceability from sensor to cloud

---

## Author

**Shilpa Kamlesh Kangya**  

---

## Future Enhancements

- Integrate QuickSight or Grafana for visualization
- Expand ML model to include time-series forecasting
- Add Step Functions for orchestrated fault recovery

---

## License

This project is for educational and portfolio purposes. All third-party tools and services are used under their respective licenses.

```
