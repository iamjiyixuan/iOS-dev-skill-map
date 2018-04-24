# Responder Chain

## 1. 事件（UIEvent）

- Touch events
- Press events
- Shake-motion events
- Remote-control events
- Editing menu messages

## 2. 响应者（UIResponder）

iOS 应用程序中只有响应者（UIResponder 的实例）可以接收和处理事件。UIApplication、UIView、UIViewController 这几个 UIKit 的核心类都是直接继承自 UIResponder。响应者接收到事件后，可以选择自己处理或者传递给下一个响应者（nextResponder）。第一个接收到事件的响应者称为第一响应者（first responder），谁是第一响应者由事件类型决定。事件沿着响应链被传递，直到被处理。

## 3. 事件通过响应链被传递

方向：子视图 → 父视图 → UIWindow → UIApplication → UIApplicationDelegate

![Responder chains in an app](https://docs-assets.developer.apple.com/published/7c21d852b9/f17df5bc-d80b-4e17-81cf-4277b1e0f6e4.png)

## 4. Hit-Testing

## 5. References
- [Understanding Event Handling, Responders, and the Responder Chain](https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/understanding_event_handling_responders_and_the_responder_chain?language=objc)