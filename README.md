# SwiftUI_chipsview

```swift

struct TagPillsAlignment: View {
    
    @State private var tags = [
        "Objective C",
        "Swift",
        "SwiftUI",
        "UIKit",
        "Combine",
    ]
    
    var body: some View {
        GeometryReader { geo in
            self.generateContent(in: geo)
        } //: GEOMETRY READER
    }
    
    private func generateContent(in geo: GeometryProxy) -> some View {
        var width = CGFloat.zero
        var height = CGFloat.zero
        
        return ZStack(alignment: .topLeading, content: {
            ForEach(self.tags, id: \.self) { item in
                self.item(for: item)
                    .padding(.all, 4)
                    .alignmentGuide(.leading) { dimension in
                        if abs(width - dimension.width) > geo.size.width {
                            width = 0
                            height -= dimension.height
                        }
                        let result: CGFloat = width
                        if item == self.tags.last! {
                            width = 0
                        } else {
                            width -= dimension.width
                        }
                        return result
                    }
                    .alignmentGuide(.top) { dimension in
                        let result: CGFloat = height
                        if item == self.tags.last! {
                            height = 0
                        }
                        return result
                    }
            } //: FOREACH

        }) //: ZSTACK
    }
    
    private func item(for text: String) -> some View {
        Text(text)
            .padding(.all, 5)
            .font(.body)
            .background(Color.orange)
            .foregroundColor(.white)
            .cornerRadius(5)
    }
    
}


```
