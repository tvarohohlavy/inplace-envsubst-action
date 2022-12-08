[![Example Pipeline](https://github.com/tvarohohlavy/inplace-envsubst-action/actions/workflows/example.yml/badge.svg)](https://github.com/tvarohohlavy/inplace-envsubst-action/actions/workflows/example.yml)

# inplace-envsubst-action
Github Action for envsubst of multiple files in place

This action allows you to substitute environment variables in files.

Will replace all $VAR / ${VAR} strings in defined files. Replacement value is taken from Environmental variables if found or empty if not.
This defualt behaviour can be overriden by "variables" option listed at the end of this file.

## Usage

### Single file
deployment.json (BEFORE)
```json
{
  "version": "${VERSION}",
  "instance": "$INSTANCE"
}
```

ACTION
```yaml
- uses: tvarohohlavy/inplace-envsubst-action@main
  env:
      VERSION: 1.2.3
      INSTANCE: staging
  with:
    files: |
      deployment.json
```


deployment.json (AFTER)
```json
{
  "version": "1.2.3",
  "instance": "staging"
}
```

### Multiple files

ACTION
```yaml
- uses: tvarohohlavy/inplace-envsubst-action@main
  env:
      VERSION: 1.2.3
      INSTANCE: staging
  with:
    files: |
      deployment.json
      test.json
      apps/Dockerfile
```


### Replace only defined variables
by listing varaibles you want to have replaced you can override default behaviour of envsubst which does replace all found $VAR / ${VAR} string even if there is no matching Environmental variable

ACTION
```yaml
- uses: tvarohohlavy/inplace-envsubst-action@main
  env:
      VERSION: 1.2.3
      INSTANCE: staging
      USER: devops
  with:
    variables: |
      $VERSION
      $INSTANCE
    files: |
      deployment.json
      test.json
      apps/Dockerfile
```
