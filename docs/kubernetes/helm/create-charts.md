---
layout: default
nav_order: 1
title: Helm Charts Creating
permalink: kubernetes/helm/helm-charts-creating/
parent: Helm
grand_parent: Kubernetes
#has_toc: true
has_children: true
---

- [Creating](#creating)


# Chart Template Guide For Custom Application

This guide covers the chart template specification and the format of the resulting chart archive. See official helm documentation [[1]].

## Language of Templates

A template directive is enclosed in `{{` and `}}`. The template language is based on the Go template language [[2]].

The values passed into the template from the `values.yaml` file starts with `.Values`. For example, `.Values.prometheus`.

The values passed into the template from the `Chart.yaml` file starts with `.Chart`. For example, `{% raw %}{{ .Chart.Name }}-{{ .Chart.Version }}{% endraw %}`.

Accesing to all non-special files in a chart are accessed with the `{{ .Files }}` object. For example to access `config.ini`, use `{{ .Files.Get "config.ini" }}`.

Other special objects are `Capabilities` and `Template`.
- `Capabilities` is a global object that holds information about the cluster's capabilities. For example: `Capabilities.KubeVersion`.
- `Template` is a global object that holds information about the template being executed. For example: `Template.Name`.


### Define Variables

You may want to define new variables.

```yaml
{{- $relname := .Release.Name -}}
```

Accessing to the variable.

```yaml
{{- $relname }}
```

### Template Functions

Most of functions are in this document: <https://helm.sh/docs/chart_template_guide/function_list/>

Actions

| Template Action | Description |
| :---: | :---: |
| `if/else` | The `if` action executes its `true` branch if the value is truthy, else it executes the `false` branch. |
| `with` | The `with` action evaluates the dot (`.`) with the given parameter and executes the nested template if the result is non-empty. |
| `range` | The `range` action iterates over an array, slice, map, or channel. |
| `define` | The `define` action creates a template with the given name. |
| `template` | The `template` action applies a named template to the pipeline and returns the result of the template invocation. |
| `block` | The `block` action defines a block that can be overridden by templates that use the `extends` action. |

Some Functions

| Template Function | Description |
| :---: | :---: |
| `default` | Returns the first argument that has a defined value. |
| `required` | Returns an error if the argument has an empty value or undefined. |
| `empty` | Returns true if the argument is empty. |
| `fail` | Returns an error with the given message. |
| `quote` | Wraps the argument in double quotes. |
| `upper` | Converts the argument to uppercase. |
| `repeat` | Repeats the string argument count times. |
| `lookup` | Returns the value associated with the given key in the given map. It is used for accesing k8s resources. |

Some operations

| Template Operations | Description |
| :---: | :---: |
| `and` | Returns the boolean truth of arg1 && arg2. |
| `or` | Returns the boolean truth of arg1 \|\| arg2. |
| `not` | Returns the boolean truth of !arg1. |
| `eq` | Returns the boolean truth of arg1 == arg2. |
| `ne` | Returns the boolean truth of arg1 != arg2. |
| `lt` | Returns the boolean truth of arg1 < arg2. |
| `le` | Returns the boolean truth of arg1 <= arg2. |
| `gt` | Returns the boolean truth of arg1 > arg2. |
| `ge` | Returns the boolean truth of arg1 >= arg2. |

### Release Object

| Template Directive | Description |
| :---: | :---: |
| `{{ .Release.Name }}` | The release name |
| `{{ .Release.Namespace }}` | The namespace into which the release is being installed |
| `{{ .Release.IsUpgrade }}` | Will be set to `true` if current operation is an upgrade |
| `{{ .Release.IsInstall }}` | Will be set to `true` if current operation is an install |
| `{{ .Release.Revision }}` | The revision number for this release. It begins at `1` and is incremented on each upgrade |
| `{{ .Release.Service }}` | The service that is rendering this template. On Helm, this is always `Helm`. |

## Creating Helm Chart Template

Following command will create a nginx helm chart template.

```bash
helm create <chart-name>
```

## Example

Create helm chart template for a custom application. [[1]].

```bash
helm create mychart
```

Change directory and remove all files in templates folder. Also remove inside of `values.yaml` file.

```bash
cd mychart
rm -rf templates/*
echo "" > values.yaml
```

Create a new file named `mychart/templates/configmap.yaml` and add following content.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
```

Here `Release` is a global object that holds information about the release. `Name` is the name of releas. It stands for the name of your installing chart.

Use `dry-run` and `debug` flags to see the output.

```bash
helm install testChart . --dry-run --debug
```

The `{{ .Release.Name }}` is replaced with the name of the release, `testChart`.

To change `Hello World` string in `values.yaml` file, change `templates/configmap.yaml` file as follows.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: {{ Values.myValue }}
```

Add `myValue` to `values.yaml` file.

```yaml
myValue: "Hello World From Values.yaml"
```

Test the output.

```bash
helm install testChart . --dry-run --debug
```

Suppose that you have two data in configmap as follows.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  drink: {{ .Values.favorite.drink }}
  food: {{ .Values.favorite.food }}
```

If you want to use more structured content like `favorite.drink` and `favorite.food` in `values.yaml` file, you should add them as follows.

```yaml
favorite:
  drink: "Soda"
  food: "Pizza"
```

If you would like to delete a key using cli, you can use `--set` flag and set the value to `null`. Following set command overrides of values in `values.yaml` file.

```bash
helm install mychart . --dry-run --debug --set favorite.drink=null
```

If you would like to use string with quotes, you should use `{{ quote .Values.myValue }}` instead of `{{ .Values.myValue }}`.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  drink: {{ quote .Values.favorite.drink }}
  food: {{ quote .Values.favorite.food }}
```

Test it.

```bash
helm install mychart . --dry-run --debug
```

Here you can see the quotes in the `data.drink` and `data.food` keys.

You can use pipeline to modify the value.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  drink: {{ .Values.favorite.drink | quote | default "Tea" }}
  food: {{ .Values.favorite.food | upper | repeat 5 }}
```

You can use `if/else` statement.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  drink: {{ .Values.favorite.drink | default "tea" | quote }}
  food: {{ .Values.favorite.food | upper | quote }}
  {{ if eq .Values.favorite.drink "coffee" }}mug: "true"{{ end }}
```

We can use loops `range` and shortcuts `with` statements. Before that, we will add a new key to `values.yaml` file.

```yaml
favorite:
  drink: "coffee"
  food: "Pizza"
pizzaToppings:
  - mushrooms
  - cheese
  - peppers
  - onions
```

Now change configmap.yaml file as follows.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-configmap
data:
  myvalue: "Hello World"
  {{- with .Values.favorite }}
  drink: {{ .drink | default "tea" | quote }}
  food: {{ .food | upper | quote }}
  release: {{ $.Release.Name }}
  {{- end }}
  toppings: |-
    {{- range .Values.pizzaToppings }}
    - {{ . | title | quote }}
    {{- end }}
```

[1]: https://helm.sh/docs/chart_template_guide/getting_started/
[2]: https://pkg.go.dev/text/template