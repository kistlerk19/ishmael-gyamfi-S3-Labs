# AWS S3 Labs - DevOps Training & Solutions Architect Associate Preparation

[![AWS](https://img.shields.io/badge/AWS-S3-orange.svg)](https://aws.amazon.com/s3/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Training](https://img.shields.io/badge/Training-DevOps-green.svg)](https://aws.amazon.com/training/)

This repository contains step-by-step instructions, deliverables, and practical exercises covering essential Amazon S3 features and best practices.

## 🎯 Learning Objectives

- Master S3 storage classes and cost optimization strategies
- Implement lifecycle policies for automated data management
- Configure versioning and MFA Delete for data protection
- Set up Cross-Region Replication for disaster recovery
- Understand S3 security and compliance requirements

## 📋 Prerequisites

### Required Access & Tools
- **AWS Account** with administrative permissions
- **AWS CLI** installed and configured (for Lab 2)
- **Sample Files**: Create test files (`test1.txt`, `test2.txt`, `test3.txt`)
- **MFA Device** (virtual or hardware) for Lab 2

### Important Setup Notes
- Use your initials in bucket names (e.g., `js-lab1-bucket-20250818`)
- Work in **us-east-1** region unless specified otherwise
- Clean up resources after each lab to avoid charges
- Document observations using provided templates

## 🧪 Laboratory Overview

### Lab 1: Storage Classes & Lifecycle Policies
**Duration:** 45 minutes  
**Focus:** Cost optimization through storage class transitions

**Key Learning Points:**
- S3 storage class comparison and pricing
- Automated lifecycle policy configuration
- Cost analysis and optimization strategies

**Deliverables:**
- ✅ Bucket with objects in different storage classes
- ✅ Lifecycle rule configuration
- ✅ Cost comparison analysis

### Lab 2: Versioning & MFA Delete
**Duration:** 60 minutes  
**Focus:** Data protection and version management

**Key Learning Points:**
- Object versioning behavior and management
- Delete markers and object restoration
- MFA Delete security implementation

**Deliverables:**
- ✅ Multiple object versions demonstration
- ✅ Delete marker behavior analysis
- ✅ MFA Delete requirements documentation

### Lab 3: Cross-Region Replication (CRR)
**Duration:** 50 minutes  
**Focus:** Disaster recovery and compliance

**Key Learning Points:**
- Cross-region replication setup and configuration
- IAM roles for replication services
- Replication behavior and limitations

**Deliverables:**
- ✅ Replication rule configuration
- ✅ Multi-region object synchronization
- ✅ Replication timing and behavior analysis

## 🗂️ Repository Structure

```
s3lab/
├── Lab1-Screenshots/          # Storage Classes & Lifecycle Policies
│   ├── Screenshot 2025-08-19 at 09.32.58.png
│   ├── Screenshot 2025-08-19 at 09.40.36.png
│   └── Screenshot 2025-08-19 at 09.45.59.png
├── Lab2-Screenshots/          # Versioning & MFA Delete
│   ├── Screenshot 2025-08-19 at 09.54.38.png
│   ├── Screenshot 2025-08-19 at 09.58.17.png
│   ├── Screenshot 2025-08-19 at 10.04.11.png
│   ├── Screenshot 2025-08-19 at 10.08.17.png
│   └── Screenshot 2025-08-19 at 10.09.16.png
├── Lab3-Screenshots/          # Cross-Region Replication
│   ├── Screenshot 2025-08-19 at 10.44.11.png
│   ├── Screenshot 2025-08-19 at 10.51.45.png
│   ├── Screenshot 2025-08-19 at 10.56.08.png
│   ├── Screenshot 2025-08-19 at 10.57.25.png
│   ├── Screenshot 2025-08-19 at 10.58.06.png
│   ├── Screenshot 2025-08-19 at 10.58.13.png
│   ├── Screenshot 2025-08-19 at 11.02.29.png
│   ├── Screenshot 2025-08-19 at 11.02.35.png
│   ├── Screenshot 2025-08-19 at 11.03.40.png
│   ├── Screenshot 2025-08-19 at 11.03.46.png
│   └── Screenshot 2025-08-19 at 11.04.19.png
├── Ishmael-Gyamfi-S3-Lab-Report.pdf
└── README.md
```

## 🚀 Quick Start Guide

### Step 1: Environment Setup
```bash
# Verify AWS CLI installation
aws --version

# Configure AWS CLI (if not already done)
aws configure

# Create test files
echo "Version 1 content" > test1.txt
echo "Version 2 content" > test2.txt
echo "Version 3 content" > test3.txt
```

### Step 2: Execute Labs in Sequence
1. **Lab 1**: Storage Classes & Lifecycle Policies
2. **Lab 2**: Versioning & MFA Delete  
3. **Lab 3**: Cross-Region Replication

### Step 3: Document and Submit
- Capture screenshots at each milestone
- Complete assessment questions
- Submit deliverables using naming convention

## 💰 Cost Optimization Insights

### Storage Class Pricing Comparison (per GB/month)
| Storage Class | Cost | Use Case |
|---------------|------|----------|
| Standard | $0.023 | Frequently accessed data |
| Standard-IA | $0.0125 + retrieval | Infrequently accessed data |
| Intelligent-Tiering | $0.023 + monitoring | Unknown access patterns |
| Glacier Flexible | $0.004 | Archive with flexible retrieval |
| Glacier Deep Archive | $0.00099 | Long-term archive |

### Lifecycle Policy Best Practices
- Transition to Standard-IA after 30 days minimum
- Use Intelligent-Tiering for unpredictable access patterns
- Archive to Glacier for compliance and backup requirements
- Set expiration policies for temporary data

## 🔒 Security & Compliance Features

### Versioning Benefits
- **Data Protection**: Prevents accidental deletion/modification
- **Compliance**: Maintains audit trail of changes
- **Recovery**: Point-in-time restoration capabilities

### MFA Delete Requirements
- Root user access only
- Hardware or virtual MFA device
- CLI-based configuration
- Enhanced security for critical operations

### Cross-Region Replication Use Cases
- **Disaster Recovery**: Geographic redundancy
- **Compliance**: Data residency requirements
- **Performance**: Reduced latency for global users
- **Analytics**: Cross-region data processing

## 🛠️ Troubleshooting Guide

### Common Issues & Solutions

#### Lab 1: Lifecycle Policies
**Issue**: "Lifecycle rule invalid"  
**Solution**: Verify minimum duration requirements (30 days for IA transitions)

#### Lab 2: Versioning
**Issue**: "Cannot enable versioning"  
**Solution**: Check bucket permissions and IAM policies

#### Lab 3: Cross-Region Replication
**Issue**: "Replication configuration invalid"  
**Solution**: Ensure versioning enabled on both source and destination buckets

**Issue**: "Access denied for replication role"  
**Solution**: Verify IAM role has proper S3 permissions

### Cleanup Commands
```bash
# Remove all object versions (use with caution)
aws s3api delete-objects --bucket [BUCKET-NAME] \
  --delete "$(aws s3api list-object-versions --bucket [BUCKET-NAME] \
  --query='{Objects: Versions[].{Key:Key,VersionId:VersionId}}')"

# Force delete bucket
aws s3 rb s3://[BUCKET-NAME] --force
```

## 📊 Assessment Questions

### Lab 1: Storage Classes & Lifecycle
1. What happens to cost when transitioning from Standard to Standard-IA?
2. Can you transition directly from Standard to Glacier Deep Archive?
3. What's the minimum duration for Standard-IA storage?

### Lab 2: Versioning & MFA Delete
1. What happens to previous versions when uploading new versions?
2. How do you permanently delete a specific object version?
3. Why can only root users enable MFA Delete?

### Lab 3: Cross-Region Replication
1. What are the prerequisites for CRR setup?
2. Do delete markers replicate by default?
3. Can you replicate within the same region?

## 📝 Submission Requirements

### Required Deliverables
1. **Screenshots** demonstrating each lab milestone
2. **Lab Report** with observations and real-world applications
3. **Cleanup Confirmation** showing resource removal

### Naming Convention
```
[YOUR-NAME]-S3-Labs/
├── Lab1-Screenshots/
├── Lab2-Screenshots/
├── Lab3-Screenshots/
└── [YOUR-NAME]-S3-Lab-Report.pdf
```

## 🎓 Certification Alignment

This lab series directly supports AWS Solutions Architect Associate exam domains:

- **Domain 1**: Design Resilient Architectures (25%)
- **Domain 2**: Design High-Performing Architectures (30%)
- **Domain 3**: Design Secure Applications and Architectures (25%)
- **Domain 4**: Design Cost-Optimized Architectures (20%)

## 🤝 Contributing

Contributions to improve lab instructions, add new scenarios, or enhance documentation are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request with detailed description

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For questions or issues:
- Review the troubleshooting guide
- Check AWS CloudTrail for detailed error messages
- Verify IAM policies and permissions
- Ensure region selections match instructions

## 🔗 Additional Resources

- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/)
- [AWS Pricing Calculator](https://calculator.aws/)
- [AWS Solutions Architect Associate Exam Guide](https://aws.amazon.com/certification/certified-solutions-architect-associate/)
- [AWS CLI S3 Commands Reference](https://docs.aws.amazon.com/cli/latest/reference/s3/)

---

**Happy Learning! 🚀**

*This repository is designed to provide hands-on experience with AWS S3 features essential for DevOps professionals and cloud architects.*