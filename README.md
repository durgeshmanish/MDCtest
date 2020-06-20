# microsoft/security-code-analysis-action

![MSCA windows-latest](https://github.com/microsoft/security-code-analysis-action/workflows/MSCA%20windows-latest/badge.svg)  
![MSCA ubuntu-latest](https://github.com/microsoft/security-code-analysis-action/workflows/MSCA%20ubuntu-latest/badge.svg)

This action runs the [Microsoft Security Code Analysis  CLI](https://aka.ms/mscadocs) for security analysis by:

* Installing the Microsoft Security Code Analysis CLI
* Installing the latest Microsoft security policy
* Installing the latest Microsoft and 3rd party security tools
* Automatic or user-provided configuration of security tools
* Execution of a full suite of security tools
* Normalized processing of results into the SARIF format
* Build breaks and more

# Usage

See [action.yml](action.yml)

## Basic

Run Guardian with the default policy and recommended tools.

```yaml
steps:
- uses: actions/checkout@v2
- uses: actions/setup-dotnet@v1
  with:
    dotnet-version: '3.1.201'
- name: Run Microsoft Security Code Analysis
  uses: Microsoft/security-code-analysis-action@master
  id: msca
- name: Upload results to Security tab
  uses: github/codeql-action/upload-sarif@v1
  with:
    sarif_file: ${{ steps.msca.outputs.sarifFile }}
```

## Upload Results to the Security tab

To upload results to the Security tab of your repo, run the `github/codeql-action/upload-sarif` action immediately after running MSCA. MSCA sets the action output variable `sarifFile` to the path of a single SARIF file that can be uploaded to this API.

```yaml
- name: Upload results to Security tab
  uses: github/codeql-action/upload-sarif@v1
  with:
    sarif_file: ${{ steps.msca.outputs.sarifFile }}
```

# License

The scripts and documentation in this project are released under the [MIT License](LICENSE)

# Contributing

Contributions are welcome! See the [Contributor's Guide](docs/contributors.md).
