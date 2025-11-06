# AI Digital Twin – Week 2 Project

This repository contains the code for building and deploying an **AI Digital Twin** — a conversational agent that acts as a digital representation of a person. Over the course of Week 2, the project evolves from a basic chat interface into a production‑ready application with memory, personalization, a serverless backend, and DevOps automation.

## Features

- **Chat interface with memory:** The twin remembers previous messages by storing conversation history in JSON files or Amazon S3.
- **Personalization:** The twin draws on custom data (facts, summaries, style notes, LinkedIn profile PDF) to answer questions in character.
- **Serverless backend:** Implemented in FastAPI and packaged for AWS Lambda with API Gateway, S3, and CloudFront.
- **Model flexibility:** Supports OpenAI models and AWS Bedrock models, with configurable model IDs.
- **Infrastructure as code:** The entire AWS stack is defined with Terraform for reproducible environments (dev, test, prod) and optional custom domains.
- **Continuous deployment:** GitHub Actions automates deploying infrastructure and code on every push.

## Getting Started

### Prerequisites

- Python 3.12
- Node.js 20+
- [uv](https://docs.astral.sh/uv/) for Python package management
- An AWS account with appropriate permissions
- AWS CLI configured locally
- Terraform 1.10+
- Docker (for packaging Lambda dependencies)
- Git

### Running Locally

1. **Clone this repository:**

   ```bash
   git clone https://github.com/your-username/twin.git
   cd twin
   ```

2. **Install backend dependencies and run the server:**

   ```bash
   cd backend
   uv init --bare
   uv python pin 3.12
   uv add -r requirements.txt
   uv run uvicorn server:app --reload
   ```

   Create a `.env` file in `backend` with your environment variables (for example, `OPENAI_API_KEY`, `CORS_ORIGINS`).

3. **Install frontend dependencies and start the development server:**

   ```bash
   cd ../frontend
   npm install
   npm run dev
   ```

   The application will run on `http://localhost:3000`.

### Deploying to AWS

For serverless deployment, follow these high‑level steps:

1. Create a `.env` file in the project root with your AWS account ID, region, OpenAI API key, and other configuration variables.
2. Build the Lambda package and deploy to AWS using the provided `backend/deploy.py` script.
3. Set up API Gateway, S3 buckets for memory and frontend, and a CloudFront distribution, either manually (as outlined in the Day 2 instructions) or via Terraform (Day 4 instructions).
4. Build a static export of the frontend and upload it to your S3 bucket.
5. Optionally, configure a custom domain and automate the entire process with GitHub Actions (Day 5 instructions).

For complete instructions, see the `week2/dayX.md` files in the `week2` directory.

## License

This project is provided for educational purposes. You may modify and use the code for your own projects. If you share your work publicly, please credit the original author.