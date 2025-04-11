---
author: John
tags: swiftui
---

After working extensively with SwiftUI, I've encountered several interesting scenarios where state updates don't trigger view updates as expected. Let me share these experiences and the lessons learned.

## The Silent Data Change Problem

One common pitfall I've encountered is when modifying underlying data doesn't trigger a view update. Here's a typical scenario:

```swift
struct PinBoard: View {
    @State private var pins: [Pin] = []
    
    var body: some View {
        VStack {
            ForEach(pins) { pin in
                PinView(pin: pin)
                    .onTapGesture {
                        deletePin(pin)
                    }
            }
        }
    }
    
    private func deletePin(_ pin: Pin) {
        pins.removeAll { $0.id == pin.id }
        // View might not update!
    }
}
```

In this example, even though we're modifying the `pins` array, SwiftUI might not detect the change because it's only watching the reference to the array, not its contents.

## The Inconsistent `removeAll` Behavior

I've noticed that `removeAll` can be particularly tricky. Sometimes it triggers updates, sometimes it doesn't. This inconsistency comes from how SwiftUI handles array mutations:

```swift
struct TodoList: View {
    @State private var todos: [Todo] = []
    
    var body: some View {
        List(todos) { todo in
            TodoRow(todo: todo)
        }
        .toolbar {
            Button("Clear All") {
                todos.removeAll() // Might work
                // vs
                todos = [] // More reliable
            }
        }
    }
}
```

The reason for this inconsistency is that `removeAll` internally uses:
```swift
mutating func removeAll(keepingCapacity keepCapacity: Bool = false) {
    self = []
}
```

While this technically modifies the array, SwiftUI's state tracking might miss this change in some scenarios.

## The ObservedObject Solution

The most reliable solution I've found is using `@ObservedObject` for complex data structures:

```swift
class PinBoardViewModel: ObservableObject {
    @Published var pins: [Pin] = []
    
    func deletePin(_ pin: Pin) {
        pins.removeAll { $0.id == pin.id }
        // This will reliably trigger updates
    }
    
    func addPin(_ pin: Pin) {
        pins.append(pin)
        // This will reliably trigger updates
    }
}

struct PinBoard: View {
    @StateObject private var viewModel = PinBoardViewModel()
    
    var body: some View {
        VStack {
            ForEach(viewModel.pins) { pin in
                PinView(pin: pin)
                    .onTapGesture {
                        viewModel.deletePin(pin)
                    }
            }
        }
    }
}
```

## Best Practices I've Learned

1. **Use `@Published` for Complex Data**
   - When dealing with arrays or objects that need internal modifications
   - When you need to track changes to nested properties

2. **Prefer Direct Assignment**
   ```swift
   // Instead of
   items.removeAll()
   
   // Use
   items = []
   ```

3. **Consider Using ViewModels**
   - Move complex state management to ObservableObject classes
   - Use `@StateObject` for view-owned view models
   - Use `@ObservedObject` for injected view models

4. **Be Explicit with State Changes**
   ```swift
   // Instead of
   pins.removeAll { $0.id == pin.id }
   
   // Consider
   pins = pins.filter { $0.id != pin.id }
   ```


These lessons have saved me countless hours of debugging and helped me create more maintainable SwiftUI applications.
