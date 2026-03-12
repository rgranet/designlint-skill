# iOS / SwiftUI Reference

## The iOS Convergence Problem

SwiftUI has its own convergence traps:
- Everything uses `.systemBackground` and `.secondarySystemBackground`
- Navigation uses default `.navigationBarTitleDisplayMode(.automatic)`
- Lists use default `List` styling (insetGrouped)
- Buttons all use `.buttonStyle(.borderedProminent)` in system blue
- Spacing follows HIG defaults everywhere, no variation
- Animations are all `.easeInOut(duration: 0.3)`

**This skill overrides all of those defaults.**

---

## Color System — Beyond System Colors

Define your palette as `Color` extensions. Never rely solely on system colors.

```swift
// Color+Brand.swift
extension Color {
    static let brandBackground    = Color(hex: "#1C1917")
    static let brandSurface       = Color(hex: "#292524")
    static let brandPrimary       = Color(hex: "#D97706")
    static let brandAccent        = Color(hex: "#FCD34D")
    static let brandText          = Color(hex: "#E7E5E4")
    static let brandTextMuted     = Color(hex: "#A8A29E")
}

extension Color {
    init(hex: String) {
        let hex = hex.trimmingCharacters(in: CharacterSet.alphanumerics.inverted)
        var int: UInt64 = 0
        Scanner(string: hex).scanHexInt64(&int)
        let r = Double((int >> 16) & 0xFF) / 255
        let g = Double((int >> 8) & 0xFF) / 255
        let b = Double(int & 0xFF) / 255
        self.init(red: r, green: g, blue: b)
    }
}
```

---

## Typography — Custom Fonts in SwiftUI

```swift
// Typography.swift
struct AppFont {
    // Display: commanding headings
    static func display(_ size: CGFloat, weight: Font.Weight = .bold) -> Font {
        .custom("PlayfairDisplay-Bold", size: size)
    }
    
    // Body: readable, warm
    static func body(_ size: CGFloat) -> Font {
        .custom("SourceSerif4-Light", size: size)
    }
    
    // Mono: labels, data, timestamps
    static func mono(_ size: CGFloat) -> Font {
        .custom("FragmentMono-Regular", size: size)
    }
    
    // Scales — break 16pt defaults
    static let displayXL  = display(44)
    static let displayLG  = display(32)
    static let headingMD  = display(22)
    static let bodyBase   = body(17)   // Not 16, not 15
    static let label      = mono(11)
    static let caption     = body(14)
}
```

**Using custom fonts**: Add to `Info.plist` under `UIAppFonts` and include in target.

For Google Fonts on iOS: download the TTF/OTF, add to project bundle.

---

## Anti-Pattern: The Generic Card

**Never:**
```swift
RoundedRectangle(cornerRadius: 12)
    .fill(Color(.secondarySystemBackground))
    .padding()
```

**Instead** (based on your DDP aesthetic):

```swift
// Brutalist: hard edges, explicit border
struct BrutalistCard<Content: View>: View {
    let content: Content
    var body: some View {
        content
            .padding(.horizontal, 20)
            .padding(.vertical, 16)
            .background(Color.brandSurface)
            .overlay(
                Rectangle()
                    .stroke(Color.brandPrimary, lineWidth: 1.5)
            )
    }
}

// Editorial: left accent bar
struct EditorialCard<Content: View>: View {
    let content: Content
    var body: some View {
        HStack(spacing: 0) {
            Rectangle()
                .fill(Color.brandAccent)
                .frame(width: 3)
            content
                .padding(.leading, 16)
                .padding(.vertical, 20)
                .padding(.trailing, 24)
        }
        .background(Color.brandSurface)
    }
}

// Luxury: generous space, no border
struct LuxuryCard<Content: View>: View {
    let content: Content
    var body: some View {
        content
            .padding(40)
            .background(Color.brandSurface)
    }
}
```

---

## Motion Character — SwiftUI Animations

**BANNED defaults**:
```swift
.animation(.easeInOut(duration: 0.3), value: state)  // Too generic
withAnimation(.default) { }  // Never use .default
```

**Snappy character:**
```swift
.animation(.spring(response: 0.25, dampingFraction: 0.8), value: state)
```

**Elastic character:**
```swift
.animation(.spring(response: 0.4, dampingFraction: 0.6), value: state)
// dampingFraction < 0.7 creates overshoot/bounce
```

**Cinematic character:**
```swift
.animation(.easeOut(duration: 0.6), value: state)
```

**Mechanical character:**
```swift
.animation(.linear(duration: 0.15), value: state)
```

**Staggered list entries:**
```swift
ForEach(Array(items.enumerated()), id: \.offset) { index, item in
    RowView(item: item)
        .opacity(appeared ? 1 : 0)
        .offset(y: appeared ? 0 : 12)
        .animation(
            .spring(response: 0.35, dampingFraction: 0.75)
                .delay(Double(index) * 0.05),
            value: appeared
        )
}
.onAppear { appeared = true }
```

---

## Navigation — Breaking the Default

**Avoid default `.navigationBarTitleDisplayMode(.automatic)`**

```swift
// Large custom header instead of nav bar
struct CustomHeader: View {
    let title: String
    var body: some View {
        VStack(alignment: .leading, spacing: 4) {
            Text(title.uppercased())
                .font(AppFont.label)
                .foregroundColor(.brandTextMuted)
                .kerning(2)
            Text(title)
                .font(AppFont.displayLG)
                .foregroundColor(.brandText)
        }
        .frame(maxWidth: .infinity, alignment: .leading)
        .padding(.horizontal, 24)
        .padding(.top, 16)
    }
}
```

**Hide system nav bar and roll your own:**
```swift
.navigationBarHidden(true)
.toolbar(.hidden, for: .navigationBar)
```

---

## Spatial Grammar — SwiftUI

**Asymmetric padding (intentional imbalance):**
```swift
.padding(.leading, 32)
.padding(.trailing, 20)
.padding(.top, 24)
.padding(.bottom, 16)
```

**Not everything should be a List. Use LazyVStack for more control:**
```swift
ScrollView {
    LazyVStack(spacing: 0) {
        ForEach(items) { item in
            RowView(item: item)
                .padding(.horizontal, 24)
                .padding(.vertical, 14)
            Divider()
                .background(Color.brandPrimary.opacity(0.2))
        }
    }
}
.background(Color.brandBackground)
```

---

## Signature Details — SwiftUI Snippets

### Accent underline for active tab
```swift
struct AccentTabBar: View {
    @Binding var selected: Int
    let tabs: [String]
    
    var body: some View {
        HStack(spacing: 0) {
            ForEach(Array(tabs.enumerated()), id: \.offset) { i, tab in
                Button(action: { selected = i }) {
                    VStack(spacing: 6) {
                        Text(tab)
                            .font(AppFont.label)
                            .foregroundColor(selected == i ? .brandText : .brandTextMuted)
                        Rectangle()
                            .fill(selected == i ? Color.brandAccent : Color.clear)
                            .frame(height: 1.5)
                            // No animation on the line — instant/physical
                    }
                }
                .frame(maxWidth: .infinity)
            }
        }
        .padding(.horizontal, 24)
    }
}
```

### Monospace data label
```swift
struct DataLabel: View {
    let value: String
    let unit: String
    
    var body: some View {
        HStack(alignment: .lastTextBaseline, spacing: 4) {
            Text(value)
                .font(AppFont.displayXL)
                .foregroundColor(.brandText)
            Text(unit)
                .font(AppFont.label)
                .foregroundColor(.brandTextMuted)
        }
    }
}
```

### Noise texture background (using SF Symbols workaround)
For grain/texture effects on iOS, use a UIKit-based approach:
```swift
struct GrainBackground: UIViewRepresentable {
    func makeUIView(context: Context) -> UIView {
        let view = UIView()
        let filter = CIFilter(name: "CIRandomGenerator")!
        let noise = CIFilter(name: "CIColorMatrix",
            parameters: [
                "inputImage": filter.outputImage!,
                "inputRVector": CIVector(x: 0, y: 0, z: 0, w: 0.04),
                "inputGVector": CIVector(x: 0, y: 0, z: 0, w: 0.04),
                "inputBVector": CIVector(x: 0, y: 0, z: 0, w: 0.04),
                "inputAVector": CIVector(x: 0, y: 0, z: 0, w: 0.04),
            ]
        )!
        // Render to UIImage and set as background
        // Implementation depends on target iOS version
        return view
    }
    func updateUIView(_ uiView: UIView, context: Context) {}
}
```

---

## Common Mistakes to Avoid in SwiftUI

| ❌ Generic | ✅ Differentiated |
|------------|------------------|
| `.listStyle(.insetGrouped)` | Custom `LazyVStack` with manual rows |
| `.foregroundStyle(.primary)` | Named token colors |
| `.buttonStyle(.borderedProminent)` | Custom `ButtonStyle` implementation |
| `NavigationStack { NavigationLink(...) }` | Custom tab/flow with `@State` |
| `.cornerRadius(12)` applied everywhere | Specific radii per context (0, 6, or 999 — not 12) |
| `Text("Title").font(.largeTitle)` | Custom font via `AppFont` |
| `Color.accentColor` | `Color.brandPrimary` |
