# Heroku buildpack: swift

This is a Heroku buildpack for Swift apps that are powered by the Swift Package Manager.

## Usage

Example usage:

```shell
$ ls
Procfile Package.swift Sources

$ heroku create --buildpack https://github.com/ChameleonBot/heroku-buildpack.git

$ git push heroku master
remote: -----> Swift app detected
remote: -----> Installing clang 5.0.0
remote: -----> Installing swiftenv
remote: -----> Installing Swift 4.0
remote: -----> Building package
remote: -----> Installing dynamic libraries
remote: -----> Installing binaries
```

You can also add it to upcoming builds of an existing application:

```shell
$ heroku buildpacks:set https://github.com/ChameleonBot/heroku-buildpack.git
```

The buildpack will detect your app as Swift if it has a `Package.swift` file in
the root.

### Procfile

Using the Procfile, you can set the process to run for your web server. Any
binaries built from your Swift source using swift package manager will
be placed in your $PATH.

Example Procfile:

```swift
web: AppName --env=production --port=$PORT
```

### Specify a Swift version

You can also customise the version of Swift used with a `.swift-version` file
in your repository:

```shell
$ cat .swift-version
3.1.1
```

The `.swift-version` file is completely compatible with
[swiftenv](http://github.com/kylef/swiftenv).

**NOTE**: *Since there are frequent Swift language changes, it's advised that
you pin to your Swift version.*

### Hooks

You can place custom scripts to be ran before and after compiling your Swift
source code inside the following files in your repository:

- `bin/pre_compile`
- `bin/post_compile`

This is useful if you would need to install any other dependencies.
