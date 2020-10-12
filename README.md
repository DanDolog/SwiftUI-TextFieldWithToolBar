# SwiftUI-TextFieldWithToolBar
Solving the problem with keyboard dismissing

Link On Introspect Library https://github.com/siteline/SwiftUI-Introspect
# CODE
```swift
import SwiftUI
import Introspect

struct TBTextField: View {
    @Binding var text: String
    var placeHolder: String
    var keyboardType: UIKeyboardType = .default
    var contentType: UITextContentType? = nil
    
    var body: some View {
        TextField(placeHolder, text: $text)
            .keyboardType(keyboardType)
            .textContentType(contentType)
            .introspectTextField { (textField) in
                let toolBar = UIToolbar(frame: CGRect(x: 0, y: 0, width: textField.frame.size.width, height: 44))
                let flexButton = UIBarButtonItem(barButtonSystemItem: UIBarButtonItem.SystemItem.flexibleSpace, target: nil, action: nil)
                let doneButton = UIBarButtonItem(title: "Done", style: .done, target: self, action: #selector(textField.doneButtonTapped(button:)))
                doneButton.tintColor = .systemPink
                toolBar.items = [flexButton, doneButton]
                toolBar.setItems([flexButton, doneButton], animated: true)
                textField.inputAccessoryView = toolBar
            }
    }
}
    
extension  UITextField{
    @objc func doneButtonTapped(button:UIBarButtonItem) -> Void {
        self.resignFirstResponder()
    }
}
```





# HOW TO USE
```swift
struct ContentView: View {
    @State var text1: String
    @State var text2: String

    var body: some View {
        Form {
            TBTextField(text: $text1,
                        placeHolder: "https://www.yeezysupply.com/product/FZN567",
                        keyboardType: .URL,
                        contentType: .URL)
                            
            TBTextField(text: $text2,
                        placeHolder: "https://www.adidas.ru",
                        keyboardType: .URL,
                        contentType: .URL)
        }
    }
}
```
