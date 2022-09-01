# jfr-static-image-action

This is a brief introduction of `jfr-static-image-action`.
It aims at running the Jenkins pipeline inside the predefined container.
If you want to learn more about the usage of this action,
you can check the [central documentation page](https://jenkinsci.github.io/jfr-action-doc).

## Inputs

| Name | Type | Default Value | Description |
| ----------- | ----------- | ----------- | ----------- |
| `command` | String | run | The command to run the [jenkinsfile-runner](https://github.com/jenkinsci/jenkinsfile-runner). The supported commands are `run` and `lint`. |
| `jenkinsfile` | String | Jenkinsfile | The relative path to Jenkinsfile. You can check [the official manual about Jenkinsfile](https://www.jenkins.io/doc/book/pipeline/syntax/). |
| `pluginstxt` | String | plugins.txt | The relative path to plugins list file. You can check [the valid plugin input format](https://github.com/jenkinsci/plugin-installation-manager-tool#plugin-input-format). You can also refer to the [plugins.txt](plugins.txt) in this repository. |
| `jcasc` | String | N/A | The relative path to Jenkins Configuration as Code YAML file. You can refer to the [demos](https://github.com/jenkinsci/configuration-as-code-plugin/tree/master/demos) provided by `configuration-as-code-plugin` and learn how to configure the Jenkins instance without using UI page. |
| `baseImage` | String | N/A | You can choose your base runtime here. By default, it will pull the Jenkinsfile-runner jdk11 prebuilt container as runtime. |

## Example

`jfr-static-image-action` is a classical docker action so the running container cannot be shared with other actions.
Therefore, the users cannot use other GitHub Actions except using `actions/checkout` to set up the workspace. 
The users can call this action by using `jenkinsci/jfr-static-image-action@master`.
```yaml
name: CI
on: [push]
jobs:
  jfr-static-image-action-pipeline:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Jenkins pipeline in the container
        uses:
          jenkinsci/jfr-static-image-action@master
        with:
          command: run
          jenkinsfile: Jenkinsfile
          pluginstxt: plugins.txt
          jcasc: jcasc.yml 
```
