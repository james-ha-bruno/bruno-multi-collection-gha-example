# Bruno CLI Multi-Collection GitHub Actions Example

This repository demonstrates how to run multiple [Bruno](https://www.usebruno.com/) API collections in GitHub Actions using the Bruno CLI. It showcases a practical approach to API testing across different services and environments in a CI/CD pipeline.

## 🎯 What This Example Shows

- **Multiple Collection Testing**: Run different Bruno collections in parallel using GitHub Actions matrix strategy
- **Environment Management**: Use different environments for each collection (prod, staging, local, etc.)
- **Test Reporting**: Generate HTML reports for each collection run
- **Artifact Collection**: Upload test results as GitHub Actions artifacts
- **Real API Testing**: Test against actual public APIs (GitHub, Cat Facts, Bruno Echo)

## 📁 Repository Structure

```
bruno-collections/
├── bruno-echo-api-collection/     # Tests Bruno's echo service
│   ├── environments/
│   │   └── Local-Env.bru         # Environment with echo API base URL
│   ├── Echo Body.bru             # POST request with JSON body
│   └── Post Car.bru              # Additional POST example
├── cat-facts-api-collection/      # Tests Cat Facts API
│   ├── environments/
│   │   └── catfacts - prod.bru   # Production environment config
│   ├── Facts/
│   │   ├── Get Random Fact.bru   # GET random cat fact
│   │   └── Get a list of facts.bru
│   └── Breeds/                   # Cat breeds endpoints
└── github-rest-api-collection/   # Tests GitHub REST API
    ├── environments/
    │   ├── Github.bru            # GitHub API environment
    │   ├── prod.bru              # Production environment
    │   └── stage.bru             # Staging environment
    ├── User/
    │   ├── User Info.bru         # GET user information
    │   └── User Repos.bru        # GET user repositories
    └── Repository/               # Repository-related endpoints
```

## 🚀 How It Works

### GitHub Actions Workflow

The workflow (`.github/workflows/CI-Bru-Cli-Demo.yml`) uses a **matrix strategy** to run each collection independently:

1. **Matrix Configuration**: Each collection is paired with its specific environment
2. **Parallel Execution**: All collections run simultaneously for faster feedback
3. **Independent Results**: Each collection generates its own test report
4. **Artifact Upload**: HTML reports are uploaded as downloadable artifacts

### Collection & Environment Mapping

| Collection | Environment | API Tested |
|------------|-------------|------------|
| `bruno-echo-api-collection` | `Local-Env` | Bruno Echo Service |
| `cat-facts-api-collection` | `catfacts - prod` | Cat Facts API |
| `github-rest-api-collection` | `Github` | GitHub REST API |

## 🛠️ Setup Instructions

### Prerequisites

- Node.js 20+ (handled automatically in GitHub Actions)
- Bruno CLI (`@usebruno/cli`)

### Local Testing

1. **Clone the repository**:
   ```bash
   git clone <your-repo-url>
   cd bruno-multi-collection-gha-example
   ```

2. **Install Bruno CLI**:
   ```bash
   npm install -g @usebruno/cli
   ```

3. **Run a specific collection**:
   ```bash
   # Navigate to a collection directory
   cd bruno-collections/cat-facts-api-collection
   
   # Run with specific environment
   bru run --env "catfacts - prod" --reporter-html results.html
   ```

4. **Run all collections** (using the same matrix approach locally):
   ```bash
   # Bruno Echo API
   cd bruno-collections/bruno-echo-api-collection
   bru run --env "Local-Env" --reporter-html results.html
   
   # Cat Facts API
   cd ../cat-facts-api-collection
   bru run --env "catfacts - prod" --reporter-html results.html
   
   # GitHub REST API
   cd ../github-rest-api-collection
   bru run --env "Github" --reporter-html results.html
   ```

## 📊 Test Results

After each workflow run:

1. **Check the Actions tab** in your GitHub repository
2. **Download artifacts** containing HTML reports for each collection
3. **View detailed results** including request/response data and assertions

## 🔧 Customization

### Adding New Collections

1. **Create a new collection** in the `bruno-collections/` directory
2. **Add environment files** in the `environments/` subdirectory
3. **Update the workflow matrix** in `.github/workflows/CI-Bru-Cli-Demo.yml`:

```yaml
matrix:
  include:
    # ... existing collections ...
    - collection: your-new-collection
      env: your-environment-name
```

### Modifying Environments

- Edit `.bru` files in each collection's `environments/` directory
- Update base URLs, variables, and authentication settings as needed
- Ensure environment names in the workflow match your `.bru` file names

### Adding Authentication

For APIs requiring authentication:

1. **Add secrets** to your GitHub repository settings
2. **Reference secrets** in the workflow using `${{ secrets.YOUR_SECRET }}`
3. **Configure authentication** in your Bruno environment files

## 🌟 Key Benefits

- **Scalable**: Easy to add new collections and environments
- **Parallel Execution**: Faster CI/CD pipeline with matrix strategy
- **Comprehensive Reporting**: HTML reports with detailed test results
- **Real-world Examples**: Tests actual public APIs for practical learning
- **Environment Flexibility**: Different configurations for different testing scenarios

## 📚 Learn More

- [Bruno Documentation](https://docs.usebruno.com/)
- [Bruno CLI Documentation](https://docs.usebruno.com/cli/overview)
- [GitHub Actions Matrix Strategy](https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs)

## 🤝 Contributing

Feel free to:
- Add more example collections
- Improve the workflow configuration
- Add more comprehensive test scenarios
- Enhance documentation

---

**Happy API Testing with Bruno! 🚀**
