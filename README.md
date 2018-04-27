[![NPM Version](https://img.shields.io/npm/v/@dscheerens/tslint-presets.svg)](https://www.npmjs.com/package/@dscheerens/tslint-presets)

# TSLint presets

This NPM package contains a number of recommended [TSLint](https://palantir.github.io/tslint/) presets.

## Installation

Install the package using the following command:

```shell
npm install --save-dev @dscheerens/tslint-presets
```

This will automatically install `tslint` as a dependency for your project.

For Angular projects it is recommended to use an Angular specific preset.
This preset makes use of [Codelyzer](http://codelyzer.com/rules/), which also need to be installed as a dependency:

```shell
npm install --save-dev codelyzer
```

## Usage

Create a new `tslint.json` in the root of your project with the following contents:

```json
{
    "extends": "@dscheerens/tslint-presets/tslint.recommended.json",
    "rules": {

    }
}
```

Use the `extends` property to specify which preset you would like to use for your project.
The different presets offered by this package are described in the next section.

You can override the tslint rules from the chosen preset by adding the custom configuration for those rules to the `rules` property.

## Available presets

This package offers the following TSLint presets:

| Preset                                             | Description                                                    |
|----------------------------------------------------|----------------------------------------------------------------|
| `tslint.recommended.json`                          | This is the default preset to use for Typescript projects.     |
| `tslint.recommended.no-type-checking.json`         | Same as previous without rules that require type checking.     |
| `tslint.recommended.angular.json`                  | Recommended rules + Codelyzer rules. Use for Angular projects. |
| `tslint.recommended.angular.no-type-checking.json` | Same as previous without rules that require type checking.     |

## Type checking

Some rules require type checking.
To support those rules run TSLint with the `--project` flag.
For more information see the [type checking documentation for TSLint](https://palantir.github.io/tslint/usage/type-checking/).

In order for your IDE to support type checking with TSLint you may want to make use of the [`tslint-language-service`](https://github.com/angelozerr/tslint-language-service) package.

> If you make use of the `tslint-language-service` and use **Visual Studio Code** as IDE, disable the **TSLint** extension to avoid that files are linted twice.
> You can disable the extension for the workshop/project only, so it won't be disabled for other projects which might not use the `tslint-language-service`.

## Best practices for TSLint

Ideally you should not override the recommended rules to make them less strict.
If you have some case in which a TSLint rule doesn't make sense it is usually best to disable that rule for the next line by adding a TSLint instruction comment, for example:

```typescript
// tslint:disable-next-line:rule-name
```

That way the rule is still enforced in other places.
If you are in the process of integrating the recommended TSLint rules in your project you might run into a lot of violations for the same rule.
In that case it is best to disable that rule for your project by adding it to the `rules` property of your `tslint.json file`, for example:

```json
{
    "extends": "@dscheerens/tslint-presets/tslint.recommended.angular.json",
    "rules": {
        "prefer-readonly": false,
        "strict-indent-size": [true, 2]
    }
}
```

Afterwards you can gradually start working on fixing the violations, until eventually you can enable the rule again by removing the override from the `tslint.json` file.
