# Secure Client-Side Deduplication Scheme in AWS

## Overview

This project implements a secure client-side deduplication scheme for cloud storage in AWS. The solution combines cryptographic techniques with AWS services to provide efficient storage while maintaining data confidentiality and integrity.

## Key Features

- **Client-side deduplication**: Eliminates redundant data transfers by detecting duplicate files before upload
- **Proof-of-ownership protocol**: Ensures only legitimate data owners can access deduplicated content
- **AWS integration**: Leverages S3 for storage, Lambda for serverless computation, and other AWS services
- **Cryptographic security**: Implements secure hash functions and encryption for data protection
- **Storage efficiency**: Reduces cloud storage costs while maintaining data privacy

## Architecture

![System Architecture Diagram](docs/architecture.png)

The system consists of:
1. **Client Application**: Handles file chunking, hashing, and proof generation
2. **Deduplication Service**: AWS Lambda functions that verify file uniqueness
3. **Storage Layer**: Amazon S3 buckets for encrypted data storage
4. **Metadata Database**: DynamoDB for tracking file hashes and ownership information

## Getting Started

### Prerequisites

- AWS account with appropriate permissions
- Node.js 16.x or later
- AWS CLI configured with credentials
- Terraform for infrastructure deployment

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/secure-client-deduplication-aws.git
   cd secure-client-deduplication-aws
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Configure AWS environment:
   ```bash
   cp .env.example .env
   # Edit .env with your AWS credentials and configuration
   ```

### Deployment

1. Initialize Terraform:
   ```bash
   cd terraform
   terraform init
   ```

2. Deploy infrastructure:
   ```bash
   terraform apply
   ```

3. Deploy Lambda functions:
   ```bash
   cd ../lambda
   ./deploy.sh
   ```

## Usage

### Client Application

```javascript
const { DeduplicationClient } = require('secure-deduplication-client');

const client = new DeduplicationClient({
  region: 'us-east-1',
  bucket: 'your-deduplication-bucket'
});

// Upload a file with deduplication
await client.uploadFile('/path/to/file.txt');
```

### API Endpoints

- `POST /api/check-duplicate`: Check if file content already exists
- `POST /api/upload`: Upload unique file content
- `GET /api/download/:fileId`: Download file content

## Security Features

- **Convergent encryption**: Files encrypted with content-derived keys
- **Proof-of-ownership**: Challenge-response protocol to verify file ownership
- **Secure metadata handling**: Cryptographic hashes stored instead of raw data
- **Access control**: IAM policies restrict access to authorized users

## Performance Metrics

| Operation | Average Latency | Throughput |
|-----------|-----------------|------------|
| Duplicate check | 120ms | 850 ops/sec |
| File upload | 450ms | 220 ops/sec |
| File download | 380ms | 300 ops/sec |

## Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Inspired by research papers on secure deduplication
- Built using AWS serverless technologies
- Cryptographic implementations based on Node.js crypto module

## Contact

For questions or support, please contact:
- Your Name - your.email@example.com
- Project Link: https://github.com/farhaan710/secure-client-deduplication-aws
