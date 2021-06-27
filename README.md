# Build and Scan Image Action

[![test workflow](https://github.com/shibataka000/build-and-scan-image-action/actions/workflows/test.yaml/badge.svg)](https://github.com/shibataka000/build-and-scan-image-action/actions/workflows/test.yaml)

Build and scan Dockerfile and container image by following tools.

- [hadolint](https://github.com/hadolint/hadolint)
- [dockle](https://github.com/goodwithtech/dockle)
- [trivy](https://github.com/aquasecurity/trivy)
- [docker scan](https://github.com/docker/scan-cli-plugin)

## Usage

### Basic

```yaml
- uses: shibataka000/build-and-scan-image-action
  with:
    tag: "shibataka000/image-name:${{ github.sha }}"
```

### All options

See [action.yaml](./action.yaml) .

```yaml
- uses: shibataka000/build-and-scan-image-action
  with:
    # Image name and optionally tag in "name:tag" format
    tag: "shibataka000/image-name:${{ github.sha }}"

    # Path to base directory to run `docker build` command (default ".")
    path: "."

    # Path to Dockerfile, which is relative path from "path" parameter (default "Dockerfile")
    dockerfile: "Dockerfile"

    # Enable scanning Dockerfile by hadolint (default "true")
    hadolint-enable: "true"

    # Hadolint version (see action.yaml to know default version)
    hadolint-version: "0.0.1"

    # Fail step if rules with a severity above this level are violated (default "info")
    # Acceptable value is one of (error|warning|info|style|ignore|none)
    hadolint-severity: "info"

    # Enable scanning image by dockle (default "true")
    dockle-enable: "true"

    # Dockle version (see action.yaml to know default version)
    docke-version: "0.0.1"

    # Fail step if checkpoints with a severity above this level are violated (default "WARN")
    # Acceptable value is one of (INFO|WARN|FATAL)
    dockle-severity: "WARN"

    # Enable scanning image by trivy (default "true")
    trivy-enable: "true"

    # Trivy version (see action.yaml to know default version)
    trivy-version: "0.0.1"

    # Fail step if image has vulnerabilities with a severity same as this level
    # (default "UNKNOWN,LOW,MEDIUM,HIGH,CRITICAL")
    # Acceptable values are some of (UNKNOWN|LOW|MEDIUM|HIGH|CRITICAL)
    trivy-severity: "UNKNOWN,LOW,MEDIUM,HIGH,CRITICAL"

    # Enable scanning image by docker scan (default "false")
    # If enabled, "docker-scan-snyk-token" must be also set. 
    docker-scan-enable: "false"

    # Docker scan version (see action.yaml to know default version)
    docker-scan-version: "0.0.1"

    # Fail step if image has vulnerabilities with a severity above this level exist (default "low")
    # Acceptable value is one of (low|medium|high)
    docker-scan-severity: "low"

    # Snyk API Token (default "")
    # This is necessary if "docker-scan-snyk-token" is "true".
    docker-scan-snyk-token: ""
```

### Ignore specific violations and vulnerabilities
Tools ([hadolint](https://github.com/hadolint/hadolint), [dockle](https://github.com/goodwithtech/dockle), [trivy](https://github.com/aquasecurity/trivy)) provide some way to ignore specific violations and vulnerabilities.

- Using configuration file
    - `.hadolint.yaml`
    - `.dockleignore`
    - `.trivyignore`
- Using inline comment (hadolint only)

See document of each tools for more details.
