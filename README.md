# LoginKit

`LoginKit` library that helps you with user logins. It provides a login screen that is customizable. It currently works with JWT tokens and Basic Auth.

[![CI Status](http://img.shields.io/travis/TigerWolf/LoginKit.svg?style=flat)](https://travis-ci.org/TigerWolf/LoginKit)
[![Version](https://img.shields.io/cocoapods/v/LoginKit.svg?style=flat)](http://cocoapods.org/pods/LoginKit)
[![License](https://img.shields.io/cocoapods/l/LoginKit.svg?style=flat)](http://cocoapods.org/pods/LoginKit)
[![Platform](https://img.shields.io/cocoapods/p/LoginKit.svg?style=flat)](http://cocoapods.org/pods/LoginKit)

## Installation

LoginKit is available through [CocoaPods](http://cocoapods.org) and [Swift Package Manager](https://swift.org/package-manager/). To install
it via CocoaPods, simply add the following line to your Podfile:

```ruby
pod "LoginKit"
```

If you want to use the latest features of `LoginKit` use normal external source dependencies.

```ruby
pod 'LoginKit', :git => 'https://github.com/TigerWolf/LoginKit.git'
```

This pulls from the `master` branch directly. We are usually careful about what we push there and this is the version we use ourselves in all of our projects.

Second, install `LoginKit` into your project:

```ruby
pod install
```

To install via Swift Package Manager, use `https://github.com/TigerWolf/LoginKit.git` as the URL and use the `.branch("master")` tag.

### Manually

* Drag the `LoginKit/LoginKit` folder into your project.
* Take care that `LoginKit.bundle` is added to `Targets->Build Phases->Copy Bundle Resources`.

## Usage

(see sample Xcode project in `/Example`)

`LoginKit` is created as a singleton (i.e. it doesn't need to be explicitly allocated and instantiated; you directly call `LoginKit.method`).

First set the config using `LoginKitConfig`

```
// Setup
LoginKitConfig.url = "https://example.com/token"
// lambda is to ensure controller is not executed until successful login.
LoginKitConfig.destination = = { ()-> UIViewController in PrivateController() }

// Load the login screen
let loginScreen = LoginKit.loginScreenController()
self.presentViewController(loginScreen, animated: false,completion: nil)
```

## Customization

`LoginKit` can be customized via the following methods:

Example:
```
Appearance.backgroundColor = UIColor(red: 0.46, green: 0.70, blue: 0.93, alpha: 1.0)
LoginKitConfig.logoImage = UIImage(named: "logo") ?? UIImage()
```

If you would like better control over tabbing between fields in your app, I would recommend `IQKeyboardManagerSwift`. This is a drop in library to add some useful features.

## Authentication

`LoginKit` assumes that every web request within the app will check for authentication (in the case of an expired token or changed password). In order to make this easy, `LoginKit` provides some utility classes for making requests to APIs which includes authentication sent with all requests as well as checks for expired tokens.

For example, after a user has logged in you can use the `LoginService` to make further network requests:

```
LoginService.request(.GET, "api/v1/beers", parameters: nil).validate()
  .responseJSON() { response in
    if response.result.isSuccess {
         let json = JSON(response.result.value!)
         // Deal with JSON response here
    }
    // Error cases are handled in LoginService
  }
```

## Compatibility

[![Swift 2.1.1 compatible](https://img.shields.io/badge/Language-Swift2-blue.svg?style=flat)](https://developer.apple.com/swift)

Minimum iOS Target: iOS 8.0

Minimum Xcode Version: Xcode 7.2

Note that for SPM support, you will need to use Swift 4 to correctly build the package.

## Contributing to this project

If you have feature requests or bug reports, feel free to help out by sending pull requests or by [creating new issues](https://github.com/TigerWolf/LoginKit/issues/new).

## License

`LoginKit` is distributed under the terms and conditions of the [MIT license](https://github.com/TigerWolf/LoginKit/blob/master/Licence.txt).

## Credits

`LoginKit` is brought to you by [Kieran Andrews](http://kieranandrews.com.au/) and [Andreas Wulf](https://github.com/awulf) and [contributors to the project](https://github.com/TigerWolf/LoginKit/contributors)
