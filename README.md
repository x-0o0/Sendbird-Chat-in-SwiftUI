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

<img src="./screenshot_1.png" width="25%" height="25%">

### How to receive event with Combine?
```swift
class ChatModel: ObservableObject {
    var proxy = SBDChannelDelegateProxy()
    var eventPublisher: AnyPublisher<ChannelEvent, Never> {
        self.proxy.passthrough.eraseToAnyPublisher()
    }
    
    // ...
}

class SBDChannelDelegateProxy: NSObject, SBDChannelDelegate {
    var passthrough = PassthroughSubject<ChannelEvent, Never>()
   
    func channel(_ sender: SBDBaseChannel, didReceive message: SBDBaseMessage) {
        guard message is SBDUserMessage else { return }
        self.passthrough.send(.didReceiveMessage(message, sender))
    }
    
    func channel(_ sender: SBDBaseChannel, messageWasDeleted messageId: Int64) {
        self.passthrough.send(.didDeleteMessage(messageId, sender))
    }
}

```
