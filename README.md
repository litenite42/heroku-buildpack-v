# Heroku Buildpack for V
![](images/vlogo.png)

This buildpack installs the most recent commit of V from [https://github.com/vlang/v](https://github.com/vlang/v).

## Installation

### Create a Heroku app with this buildpack

```sh
$ heroku create --buildpack https://github.com/louis77/heroku-buildpack-v.git
```

### Set the buildpack for an existing Heroku app

```sh
$ heroku buildpacks:set https://github.com/louis77/heroku-buildpack-v.git
```


## Getting started

To deploy a V app, your repo should contain at minimum these files:

```shell
app.v
vpm.txt
```

`app.v` will be compiled and run on deploy.

`vpm.txt`is a list of VPM modules that will be installed using `v install ...` before your app is compiled. List one module per line and *terminate with a new line*:

```
nedpals.jsonrpc
nedpals.args
```

You can omit `vpm.txt`, no packages will be installed then.

Find available VPM modules in the [VPM modules directory](https://vlang.io/modules).

`remote.txt` is a list of remote git repo urls and their module name that will be installed using `git clone remote_url ~/.vmodules/module_name` before your app is compiled. List one repo and module name per line separated by a space and *terminate with a new line*:

```
https://www.github.com/username/repo_name.git module_name
https://some_other_url/username/another_repo.git module_name_too
```

creates the following directories:
```
~/.vmodules/module_name
~/.vmodules/module_name_too
```

You can omit `remote.txt`, no repos will be cloned then.

### Procfile

If there is no Procfile in the base directory of the code being built, then a default Procfile is created that that looks like this:

```
web: ./app
```

## Hacking on this buildpack

To change this buildpack, fork it on GitHub & push changes to your fork. Contributions are very welcome!

## TODO

- [ ] Support to define desired commit/branch of V
- [ ] Cache compiled V binary
- [ ] Cache installed modules
- [ ] Add config facility

## Credits

© Louis Brauer under The MIT License. Feel free to do whatever you want with it.
