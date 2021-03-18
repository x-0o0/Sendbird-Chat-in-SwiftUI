# Sendbird-Chat-in-SwiftUI

![SwiftUI 2](https://img.shields.io/badge/SwiftUI_2-e4405f?style=for-the-badge&logo=swift&logoColor=white)

## Tips

### How to draw chat UI?
By using `.rotationEffect(Angle(degrees: 180))` twice, you can make message bubbles align to the bottom.

```swift
ScrollView(showsIndicators: false) {
    LazyVStack {
        // Align to the bottom
        Spacer()
                    
        // Draw bubbles
        ForEach(messages) {
            MessageBubble(message: $0)
        }
    }
    .rotationEffect(Angle(degrees: 180))
}
.rotationEffect(Angle(degrees: 180))
```

<img src="./screenshot_1.png" width="50%" height="50%">
