# Postman API Testing

This repository contains automated API tests for various endpoints using Postman collections, environments, and GitHub Actions for CI/CD. It is designed to validate API functionality, automate regression checks, and generate detailed test reports.

## Project Structure

```text
.
├── Task-Management-API.postman_collection.json
├── practice-dev.postman_environment.json
├── api-test-results.csv
├── detailed-report.html
├── postman-report.html
├── tests/
│   └── postman/
│       ├── CRUD-Chain.postman_collection.json
│       ├── dataset.json
│       └── social-prod.postman_environment.json
└── .github/
    └── workflows/
        ├── newman-test.yml
        └── postman-test.yml
```

### Key Files

- **Task-Management-API.postman_collection.json**: Main Postman collection for task management API tests.
- **practice-dev.postman_environment.json**: Environment variables for development/testing (e.g., `baseURL`).
- **api-test-results.csv**: CSV summary of test results.
- **detailed-report.html** & **postman-report.html**: Human-readable HTML reports generated after test runs.
- **tests/postman/CRUD-Chain.postman_collection.json**: Advanced CRUD chain tests for product APIs.
- **tests/postman/dataset.json**: Sample data for use in tests.
- **tests/postman/social-prod.postman_environment.json**: Environment for production-like API testing.
- **.github/workflows/**: Contains GitHub Actions workflows for automated testing.

## Setup

### Prerequisites

- Node.js (v20+ recommended)
- npm
- [Newman](https://www.npmjs.com/package/newman) (Postman CLI runner)
- Postman account (for API key if using cloud-based CLI)
- GitHub repository secrets for CI (see below)

### Local Test Execution

1. **Install Newman and Reporters:**

   ```sh
   npm install -g newman newman-reporter-markdown newman-reporter-htmlextra
   ```

2. **Run a Collection Locally:**

   ```sh
   newman run Task-Management-API.postman_collection.json -e practice-dev.postman_environment.json -r cli,markdown,htmlextra
   ```

   - Reports will be generated in the current directory.

3. **Advanced Test Suite:**

   ```sh
   newman run ./tests/postman/CRUD-Chain.postman_collection.json -e ./tests/postman/social-prod.postman_environment.json -r cli,markdown,htmlextra
   ```

### GitHub Actions CI/CD

#### 1. **newman-test.yml**

- Runs on every push or PR to `main`.
- Installs Node.js, Newman, and reporters.
- Executes the CRUD-Chain collection and uploads reports as workflow artifacts.

#### 2. **postman-test.yml**

- Uses the official Postman CLI GitHub Action.
- Requires the following repository secrets:
  - `POSTMAN_API_KEY`: Your Postman API key.
  - `POSTMAN_COLL_ID`: Collection ID from Postman.
  - `POSTMAN_ENV_ID`: Environment ID from Postman.

- Generates and uploads an HTML report after each run.

## Reports

- **CSV**: `api-test-results.csv` provides a summary of test results.
- **HTML**: `detailed-report.html` and `postman-report.html` are detailed, human-friendly reports.
- **Artifacts**: GitHub Actions uploads HTML reports for each run.

## Data-Driven Testing

- The `dataset.json` file in `tests/postman/` contains sample product data for use in parameterized tests.

## Example Test Cases

- **Task-Management-API**: Validates endpoints like "Get All Tasks" and "Mock Login".
- **CRUD-Chain**: End-to-end product creation, ID extraction, and state management.

## Contributing

1. Fork the repo and create a feature branch.
2. Add or update Postman collections/environments.
3. Update or add tests and datasets as needed.
4. Commit and push your changes.
5. Open a pull request.
