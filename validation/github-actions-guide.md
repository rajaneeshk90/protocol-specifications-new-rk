# GitHub Actions Integration

## Running Validation Locally

All validation tools can be run standalone on your local machine without GitHub Actions.

**Spectral validation:**
```bash
cd validation/spectral
npm install
npm run lint
```

## GitHub Actions Integration

The validation is also integrated with GitHub Actions to automatically check every pull request and push to `main`/`master` branches.

The workflow is defined in `.github/workflows/validate-style.yml`. When triggered, it:
1. Sets up Node.js environment
2. Installs Spectral CLI
3. Runs validation against all OpenAPI files
4. Reports pass/fail status on the PR

If validation fails, the PR will show a failed check, prompting the author to fix the issues before merging.

## Future: Node.js Validation

When Phase 2 Node.js validation is implemented (for JSON-LD, profile.json, and cross-file checks), it will follow the same pattern:
- Run locally via `npm run validate` in the `validation/nodejs` directory
- Integrate with GitHub Actions as an additional job in the workflow

This ensures all validation—whether Spectral or Node.js—can be run both locally during development and automatically in CI/CD.
