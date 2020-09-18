NOTE: This repo was forked by masschallenge to get around a build failure, tracked in AC-8193

The build failure occurred when this repo's setup.py was executed by our buildout. Error output follows:

```
We have no distributions for bullet-train that satisfies 'bullet-train'.Getting distribution for 'bullet-train'.Fetching bullet-train 1.0.5 from: https://files.pythonhosted.org/packages/01/ab/e14e7788f5980116556ca34df6594673e802b526d1741e6257e499e675c7/bullet-train-1.0.5.tar.gz#sha256=f229f7f544edab0122cc027e488fd037f814421c42bc0ce7df10d89216a593d0Running easy_install:"/usr/bin/python3.6" "-c" "import sys; sys.path[0:0] = ['/usr/local/lib/python3.6/dist-packages']; from setuptools.command.easy_install import main; main()" "-mZUNxd" "/srv/www/mc/current/eggs/tmpibfgcf9c" "/tmp/tmpexzqsofsget_dist/bullet-train-1.0.5.tar.gz"path=['/usr/local/lib/python3.6/dist-packages']

Processing bullet-train-1.0.5.tar.gz
Writing /tmp/easy_install-h_hquola/bullet-train-1.0.5/setup.cfg
Running bullet-train-1.0.5/setup.py -q bdist_egg --dist-dir /tmp/easy_install-h_hquola/bullet-train-1.0.5/egg-dist-tmp-kwoubpe2
error: [Errno 2] No such file or directory: 'Readme.md'
An error occurred when trying to install /tmp/tmpexzqsofsget_dist/bullet-train-1.0.5.tar.gz. Look above this message for any errors that were output by easy_install.
While:
  Installing python.
  Getting distribution for 'bullet-train'.

An internal error occurred due to a bug in either zc.buildout or in a
recipe being used:
```

We have made no behavioral changes to this repo, and will return to the main line when we have either figured out the build issue or find a version that builds without this error in our buildout process. 

<img width="100%" src="https://raw.githubusercontent.com/SolidStateGroup/bullet-train-frontend/master/hero.png"/>

# Bullet Train Client

The SDK clients for Python [https://bullet-train.io/](https://www.bullet-train.io/). Bullet Train allows you to manage feature flags and remote config across multiple projects, environments and organisations.

For full documentation visit [https://docs.bullet-train.io](https://docs.bullet-train.io)**

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See running in production for notes on how to deploy the project on a live system.

## Installing

### VIA pip

```bash
pip install bullet-train
```

## Usage

### Retrieving feature flags for your project

```python
from bullet_train import BulletTrain;

bt = BulletTrain(environment_id="<YOUR_ENVIRONMENT_KEY>")

if bt.has_feature("header", '<My User Id>'):
  if bt.feature_enabled("header"):
    # Show my awesome cool new feature to the world

if bt.has_feature("header"):
  if bt.feature_enabled("header"):
    # Show my awesome cool new feature to the world

value = bt.get_value("header", '<My User Id>')

value = bt.get_value("header")

bt.set_trait("accept-cookies", "true", "ben@bullet-train.io"))
bt.get_trait("accept-cookies", "ben@bullet-train.io"))
```

### Available Options

| Property        | Description           | Required  | Default Value  |
| ----- |:-------------| -----:| -----:|
| ```environment_id```     | Defines which project environment you wish to get flags for. *example ACME Project - Staging.* | **YES** | None
| ```api```     | Use this property to define where you're getting feature flags from, e.g. if you're self hosting. |  **NO** | https://api.bullet-train.io/api/

### Available Functions

| Function        | Description |
| ------------- |:-------------:|
| ```has_feature(key)```     | Determine if given feature exists for an environment. ```bt.has_feature("powerUserFeature") // true```
| ```feature_enabled(key)```     | Get the value of a particular *feature flag* e.g. ```bt.feature_enabled("powerUserFeature") // true```
| ```feature_enabled(key, userId)```     | Get the value of a particular *feature flag* e.g. ```bt.feature_enabled("powerUserFeature", 1234) // true```
| ```get_value(key)```     | Get the value of a particular *remote config* e.g. ```bt.get_value("font_size") // 10```
| ```get_value(key, userId)```     | Get the value of a particular feature for a specified user e.g. ```bt.get_value("font_size", 1234) // 15```
| ```set_trait(trait_key, trait_value, userId)```     | Set the value of a particular trait for a specified user e.g. ```bt.set_trait("font_size", 12, 1234) // 15```
| ```get_trait(trait_key, userId)```     | Get the value of a particular trait for a specified user e.g. ```bt.get_trait("font_size", 1234) // 12```
| ```get_flags()```     | Trigger a manual fetch of the environment features, returns a list of flag objects, see below for returned data
| ```get_flags_for_user(1234)```     | Trigger a manual fetch of the environment features with a given user id, returns a list of flag objects, see below for returned data

### Identifying users

Identifying users allows you to target specific users from the [Bullet Train dashboard](https://www.bullet-train.io/).
You can include an optional user identifier as part of the `has_feature` and `get_value` methods to retrieve unique user flags and variables.

### Flags data structure

| Field | Description | Type |
| ---- | ------------ | ---- |
| id | Internal id of feature state | Integer |
| enabled | Whether feature is enabled or not | Boolean |
| environment | Internal ID of environment | Integer | 
| feature_state_value | Value of the feature | Any - determined based on data input on [bullet-train.io](https://bullet-train.io). |
| feature | Feature object - see below for details | Object |

### Feature data structure

| Field | Description | Type |
| ---- | --------------- | --- |
| id | Internal id of feature | Integer |
| name | Name of the feature (sometimes referred to as key or ID) | String |
| description | Description of the feature | String |
| type | Feature Type. Can be FLAG or CONFIG | String |
| created_date | Date feature was created | Datetime |
| inital_value | The initial / default value set for all feature states on creation | String |
| project | Internal ID of the associated project | Integer |  

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/kyle-ssg/c36a03aebe492e45cbd3eefb21cb0486) for details on our code of conduct, and the process for submitting pull requests to us.

## Getting Help

If you encounter a bug or feature request we would like to hear about it. Before you submit an issue please search existing issues in order to prevent duplicates.

## Useful links

[Website](https://bullet-train.io)

[Documentation](https://docs.bullet-train.io/)

[Code Examples](https://github.com/SolidStateGroup/bullet-train-docs)

[Youtube Tutorials](https://www.youtube.com/channel/UCki7GZrOdZZcsV9rAIRchCw)
