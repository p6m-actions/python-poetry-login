# Python Poetry Login

![Latest Release](https://img.shields.io/github/v/release/p6m-actions/python-poetry-login?style=flat-square&label=Latest%20Release&color=blue)

## Description

A GitHub Action that logs in to one or more Python repositories using Poetry. This action allows you to configure multiple repository URLs and their corresponding authentication credentials for use with Poetry.

## Usage

Add this action to your workflow to configure Poetry with repository URLs and authentication credentials:

```yaml
- uses: p6m-actions/python-poetry-login@v1
  with:
    upload-urls: |
      pypi=https://upload.pypi.org/legacy/
      private=https://private.registry.com/
    credentials: |
      pypi=username:password
      private=user:pass
```

## Inputs

| Input         | Description                                                                  | Required |
| ------------- | ---------------------------------------------------------------------------- | -------- |
| `upload-urls` | Registry URL mappings in `registry=url` format. One per line.                | No       |
| `credentials` | Authentication credentials in `registry=user:password` format. One per line. | Yes      |

## Examples

### Basic Authentication with PyPI

```yaml
- name: Setup Poetry
  uses: p6m-actions/python-poetry-setup@v1
- name: Login to PyPI
  uses: p6m-actions/python-poetry-login@v1
  with:
    credentials: |
      pypi=username:password
```

### Multiple Repositories

```yaml
- name: Setup Poetry
  uses: p6m-actions/python-poetry-setup@v1
- name: Login to Python Repositories
  uses: p6m-actions/python-poetry-login@v1
  with:
    upload-urls: |
      pypi=https://upload.pypi.org/legacy/
      private=https://private.registry.com/
    credentials: |
      pypi=username:password
      private=user:pass
```

## Security Note

It's recommended to use GitHub Secrets for storing credentials:

```yaml
- uses: p6m-actions/python-poetry-login@v1
  with:
    credentials: |
      pypi=${{ secrets.PYPI_CREDENTIALS }}
      private=username:${{ secrets.PRIVATE_REPO_PASSWORD }}
```
