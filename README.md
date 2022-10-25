# telemetry-canary-resources

[![Brought to you by Telemetry Team](https://img.shields.io/badge/MDTP-Telemetry-40D9C0?style=flat&labelColor=000000&logo=gov.uk)](https://confluence.tools.tax.service.gov.uk/display/TEL/Telemetry)

## Table of Contents
* [Overview](#Overview)
* [Linking the repository](#Linking-the-repository)
* [Updating the repository](#Updating-the-repository)
* [References](#References)
* [License](#License)

## Overview
This repository contains [cookiecutter](https://github.com/cookiecutter/cookiecutter) template resources for Telemetry AWS
Canary repositories. Only long-term, common and stable files should be added, e.g. scripts or configurations that, when
the need to be changed, they can be changed in unison. It is worth noting that files in this template repository can be
overridden in the repository using the templates. Simply add the file to a skip list defined in the `pyproject.toml` in
the canary repo.

```toml
[tool.cruft]
skip = [".bandit"]
```

## Linking the repository

The repository is meant to be used as a cookiecutter source inside the `aws-canary-telemetry-*` repos. To add the templates
to the consuming repository, follow the procedure below.

```shell
# Update project
git checkout --branch TEL-3093-add-cruft
poetry update
poetry add --group dev cruft cookiecutter
```

For the next step, navigate to the folder above. **Note:** this is important as the cruft create will use the
`cruft_repo_name` property to insert the templated files, overwriting where necessary, into the actual project folder

```shell
# This is an example to demonstrate the commands, your folders will be different
pwd # ~/source/hmrc/aws-canary-telemetry-grafana
cd ..
pwd # ~/source/hmrc
cruft create --overwrite-if-exists https://github.com/hmrc/telemetry-canary-resources
# At the `cruft_repo_name` prompt make sure you enter `aws-canary-telemetry-grafana` to target the correct project
cd -
pwd # ~/source/hmrc/aws-canary-telemetry-grafana
git add .
```

```shell
# Link the templates repository
cruft link https://github.com/hmrc/telemetry-canary-resources # Carefully enter the properties into the prompts

# Run update (this doesn't patch up local files with the contents of the templates repository)
cruft update

# Run a diff and apply those changes (this does patch up local files)
cruft diff | git apply
```

## Updating the repository

```shell
cruft check
cruft diff
cruft update --skip-apply-ask

# If the update does not work - an update can be forced
cruft diff | git apply
```

## References

* [Cruft](https://cruft.github.io/cruft)
* [Cookiecutter](https://cookiecutter.readthedocs.io/en/stable/)

## License

This code is open source software licensed under the [Apache 2.0 License]("http://www.apache.org/licenses/LICENSE-2.0.html").
