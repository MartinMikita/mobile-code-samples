# MapTiler Mobile Code Samples

This repo contains simple code samples along with tutorial showing how to get started with MapBox SDK and MapTiler cloud. There are versions of this tutorial for iOS (UIKit and SwiftUI) and Android.

## Samples

Each sample contains two markdown files:
1. `README.md` describes how to configure, compile and run the sample
2. `TUTORIAL.md` contains tutorial fo the given platform

List of code samples:

* iOS
    * [SwiftUI](ios-swiftui/README.md)
    * [SwiftUI - Tutorial](ios-swiftui/TUTORIAL.md)
    * [UIKit](ios-uikit/README.md)
    * [UIKit - Tutorial](ios-uikit/TUTORIAL.md)
* Android
    * [Android](android/README.md)
    * [Android - Tutorial](android/TUTORIAL.md)


## Note for maintainers - code snippets extraction

The repo contains toolset for extracting code snippets from source code and updating markdown templates.
There is one tool for Swift and another for Android in build-tools sub folder.
These are command line tools. The source code is included in this repo - for swift is `build-tools/swift-extractor` and for android `build-tools/android-extractor.` Binaries are included in `build-tools/{tool-name}/bin` folder along with wrapper script.

The setup instructions are written here: [build tools setup instructions](build-tools/README.md)

The root script is `build-tools/update-markdown-documents.sh`. The process takes `TUTORIAL_TEMPLATE.md` template in the sample sub folder, extract all tokens with `snippet(fileName#tokenName)` format - the token value is the string within brackets. In the source code, snippets are marked by comments with format `// snippet(tokenValue)`. The toolset substitutes each token with the value found in the source code. 

For example, if there is text like this in markdown template:

```markdown
# My Markdown File

## Code Sample

The sample text

    ```kotlin
    snippet(SourceCodeFile.kt#MySnippet)
    ```

```

The toolset parses `SourceCodeFile.kt`, into syntax tree, locates the comment (MySnippet) and finds the closest code block below this comment.
So if there is code like this in `SourceCodeFile.kt`

```kotlin
class Person(firstName: String, lastName: String, yearOfBirth: Int) {
    val fullName = "$firstName $lastName"
    var age: Int
    
    // snippet(MySnippet)
    init {
        age = 2018 - yearOfBirth
    }
}
```

The token in markdown example above get substituted as follows:

```markdown
# My Markdown File

## Code Sample

The sample text

    ```kotlin
    init {
        age = 2018 - yearOfBirth
    }
    ```

```



