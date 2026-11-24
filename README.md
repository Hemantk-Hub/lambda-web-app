# aws-serverless-webapp

A serverless web application deployed on AWS. It uses **AWS Lambda** for backend logic, **Amazon API Gateway** to expose REST endpoints, and **Amazon DynamoDB** as the database. There are no servers to manage, and the app scales automatically with traffic.

## Architecture

```
Client → API Gateway → Lambda → DynamoDB
```

1. The client sends an HTTP request to API Gateway.
2. API Gateway triggers the Lambda function.
3. Lambda reads from or writes to DynamoDB and returns a response.

## Tech Stack

- AWS Lambda ([Python / Node.js])
- Amazon API Gateway (REST API)
- Amazon DynamoDB
- [AWS SAM / Serverless Framework / Terraform] for deployment

## Features

- Create, read, update, and delete items through a REST API
- Pay-per-use pricing and automatic scaling
- Infrastructure defined as code

## Prerequisites

- An AWS account
- AWS CLI installed and configured (`aws configure`)
- [Node.js / Python] installed
- [AWS SAM CLI / Serverless Framework / Terraform] installed

## Project Structure

```
aws-serverless-webapp/
├── src/            # Lambda function code
├── template.yaml   # Infrastructure definition
├── tests/          # Unit tests
└── README.md
```

## Deployment

```bash
# 1. Clone the repository
git clone https://github.com/[your-username]/aws-serverless-webapp.git
cd aws-serverless-webapp

# 2. Build and deploy (example using AWS SAM)
sam build
sam deploy --guided
```

After deployment, the API URL is shown in the output.

## API Endpoints

| Method | Endpoint       | Description        |
|--------|----------------|--------------------|
| GET    | `/items`       | List all items     |
| GET    | `/items/{id}`  | Get one item       |
| POST   | `/items`       | Create an item     |
| PUT    | `/items/{id}`  | Update an item     |
| DELETE | `/items/{id}`  | Delete an item     |

## Example Request

```bash
curl -X POST https://[api-id].execute-api.[region].amazonaws.com/items \
  -H "Content-Type: application/json" \
  -d '{"name": "Sample item"}'
```

## Clean Up

To avoid AWS charges, delete the resources when you're done:

```bash
sam delete
```

## Troubleshooting

- **`Internal server error`:** check the Lambda function's logs in CloudWatch.
- **`Access denied`:** confirm the Lambda's IAM role has permission to access DynamoDB.

## License

This project is licensed under the [MIT License](LICENSE).
