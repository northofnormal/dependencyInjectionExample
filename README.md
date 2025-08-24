```
import SwiftUI

enum SomeAction {
    case one
    case two
}

struct OriginalView: View {

    var body: some View {
        InjectedView(viewModel: SomeViewModel { action in
            switch action {
            case .one:
                print("1️⃣")
            case .two:
                print("two!")
            }
        })
    }
}


class SomeViewModel: ObservableObject {
    var someAction: (SomeAction) -> Void

    init(action: @escaping (SomeAction) -> Void) {
        someAction = action
    }
}

struct InjectedView: View {
    @ObservedObject var viewModel: SomeViewModel

    var body: some View {
        VStack {
            Button {
                viewModel.someAction(.one)
            } label: {
                Text("One")
            }

            Button {
                viewModel.someAction(.two)
            } label: {
                Text("Two")
            }
        }
    }
}

```
