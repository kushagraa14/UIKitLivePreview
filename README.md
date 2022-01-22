# UIKitLivePreview

Enables SwiftUI live previews for UIKit views and view controllers.

![uikitlivepreview720](https://user-images.githubusercontent.com/4868132/116438635-377b3100-a881-11eb-9a6c-34698b524848.gif)

## Requirements

- macOS Catalina or later
- Xcode 12 or later
- iOS Deployment Target 12.0 or later

## Installation

### Swift Package Manager (Recommended)

In Xcode 13 or later, select **File > Add Packages...** 

In Xcode 12, select **File > Swift Packages > Add Package Dependency...**

Add `https://github.com/nicoelayda/UIKitLivePreview.git` as the package repository URL.

**or**

If you have an existing `Package.swift` file, add `UIKitLivePreview` package to your target's dependencies.

```swift
dependencies: [
    .package(url: "https://github.com/nicoelayda/UIKitLivePreview.git", .upToNextMajor(from: "1.3.0"))
]
```

### Carthage

1. Add `UIKitLivePreview` to your `Cartfile`.

    ```
    github "nicoelayda/UIKitLivePreview" ~> 1.3.0
    ```

2. Run `carthage update --use-xcframeworks`
3. Drag `UIKitLivePreview.xcframework` in `Carthage/Build` into your application target's **Frameworks, Libraries and Embedded Content**.

### Cocoapods

1. Add `UIKitLivePreview` to your `Podfile`.

    ```ruby
    pod 'UIKitLivePreview', '~> 1.3.0'
    ```

2. Run `pod install`

### Manual Install

Copy the contents of [`Sources/UIKitLivePreview`](https://github.com/nicoelayda/UIKitLivePreview/tree/main/Sources/UIKitLivePreview) to your project.

A prebuilt [XCFramework binary](https://github.com/nicoelayda/UIKitLivePreview/releases/latest) is also available

## Usage
1. Import `UIKitLivePreview` in your view or view controller.
2. In the same Swift file, define a new struct conforming to `PreviewProvider`.
3. Inside the `previews` property:
    - Initialise your UIKit view or view controller.
    - Call `preview()` on it to create a wrapped SwiftUI `View` instance.
    - Return the preview instance.
4. Optionally, you may chain `ViewModifier`s to customise the preview. See example below.
    
#### Example
    
```swift

final class MyViewController: UIViewController { /* ... */ }

#if DEBUG && canImport(SwiftUI)
import SwiftUI

@available(iOS 13.0, *)
struct MyViewController_Preview: PreviewProvider {
    static var previews: some View {
        MyViewController()
            .preview()
            .device(.iPhone11)
            .landscape()
    }
}
#endif
```

**NOTE:** If your project is targeting iOS 12, it is recommended to wrap the `PreviewProvider` struct in a `#if canImport(SwiftUI)` directive and add the `@available(iOS 13.0, *)` attribute to it.

Check out [**UIKitLivePreview-Examples**](https://github.com/nicoelayda/UIKitLivePreview-Examples) for a sample project.

## License

MIT. See [LICENSE](https://github.com/nicoelayda/UIKitLivePreview/blob/main/LICENSE).

