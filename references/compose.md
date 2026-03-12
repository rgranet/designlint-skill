# Android / Jetpack Compose Reference

## The Compose Convergence Problem

Jetpack Compose has its own convergence traps:
- Everything uses `MaterialTheme.colorScheme` defaults (Material You purple)
- Navigation uses default `NavigationBar` with 5 `NavigationBarItem`s
- Lists always use `LazyColumn` with `Card(shape = RoundedCornerShape(12.dp))`
- Buttons use `Button(onClick = ...)` with Material3 default styling
- Spacing follows `16.dp` padding everywhere
- Animations are all `animateFloatAsState` with default spring

**This skill overrides all of those defaults.**

---

## Color System — Beyond Material You

Define a custom color scheme. Never rely solely on `MaterialTheme.colorScheme`.

```kotlin
// BrandColors.kt
object BrandColors {
    val background    = Color(0xFF1C1917)  // warm black
    val surface       = Color(0xFF292524)  // dark stone
    val primary       = Color(0xFFD97706)  // amber
    val accent        = Color(0xFFFCD34D)  // gold
    val text          = Color(0xFFE7E5E4)  // warm white
    val textMuted     = Color(0xFFA8A29E)  // stone
}

// Wrap in a CompositionLocal for theming
val LocalBrandColors = staticCompositionLocalOf { BrandColors }
```

### Custom MaterialTheme Override

```kotlin
@Composable
fun BrandTheme(content: @Composable () -> Unit) {
    val colors = darkColorScheme(
        background = BrandColors.background,
        surface = BrandColors.surface,
        primary = BrandColors.primary,
        onPrimary = BrandColors.background,
        onBackground = BrandColors.text,
        onSurface = BrandColors.text,
    )
    MaterialTheme(
        colorScheme = colors,
        typography = BrandTypography,
        content = content
    )
}
```

---

## Typography — Custom Fonts in Compose

```kotlin
// BrandTypography.kt
val PlayfairDisplay = FontFamily(
    Font(R.font.playfair_display_bold, FontWeight.Bold)
)
val SourceSerif4 = FontFamily(
    Font(R.font.source_serif_4_light, FontWeight.Light),
    Font(R.font.source_serif_4_regular, FontWeight.Normal),
    Font(R.font.source_serif_4_semibold, FontWeight.SemiBold),
)
val FragmentMono = FontFamily(
    Font(R.font.fragment_mono_regular, FontWeight.Normal)
)

val BrandTypography = Typography(
    displayLarge = TextStyle(
        fontFamily = PlayfairDisplay,
        fontWeight = FontWeight.Bold,
        fontSize = 44.sp,
        lineHeight = 44.sp,        // tight — not default 52sp
        letterSpacing = (-0.03).em,
    ),
    headlineMedium = TextStyle(
        fontFamily = PlayfairDisplay,
        fontWeight = FontWeight.Bold,
        fontSize = 22.sp,
        lineHeight = 26.sp,
    ),
    bodyLarge = TextStyle(
        fontFamily = SourceSerif4,
        fontWeight = FontWeight.Light,
        fontSize = 17.sp,          // Not 16sp
        lineHeight = 28.sp,        // 1.65 ratio — intentional
    ),
    labelSmall = TextStyle(
        fontFamily = FragmentMono,
        fontWeight = FontWeight.Normal,
        fontSize = 11.sp,
        letterSpacing = 0.12.em,
    ),
)
```

---

## Anti-Pattern: The Generic Card

**Never:**
```kotlin
Card(
    shape = RoundedCornerShape(12.dp),
    colors = CardDefaults.cardColors(containerColor = MaterialTheme.colorScheme.surface),
    elevation = CardDefaults.cardElevation(defaultElevation = 2.dp),
) { /* ... */ }
```

**Instead** (based on your DDP aesthetic):

```kotlin
// Brutalist: no radius, explicit border
@Composable
fun BrutalistCard(content: @Composable () -> Unit) {
    Box(
        modifier = Modifier
            .border(1.5.dp, BrandColors.primary)
            .background(BrandColors.surface)
            .padding(horizontal = 20.dp, vertical = 16.dp)
    ) { content() }
}

// Editorial: left accent bar
@Composable
fun EditorialCard(content: @Composable () -> Unit) {
    Row(modifier = Modifier.background(BrandColors.surface)) {
        Box(
            modifier = Modifier
                .width(3.dp)
                .fillMaxHeight()
                .background(BrandColors.accent)
        )
        Box(
            modifier = Modifier
                .padding(start = 16.dp, top = 20.dp, end = 24.dp, bottom = 20.dp)
        ) { content() }
    }
}

// Luxury: generous space, no border, no elevation
@Composable
fun LuxuryCard(content: @Composable () -> Unit) {
    Box(
        modifier = Modifier
            .background(BrandColors.surface)
            .padding(40.dp)
    ) { content() }
}
```

---

## Motion Character — Compose Animations

**BANNED defaults:**
```kotlin
animateFloatAsState(targetValue, animationSpec = spring())  // default spring is generic
animateContentSize()  // with no spec is invisible
```

**Snappy character:**
```kotlin
val animSpec = spring<Float>(
    dampingRatio = Spring.DampingRatioNoBouncy,
    stiffness = 800f  // high stiffness = fast
)

// Or for Dp/Offset:
val offsetSpec = spring<Dp>(
    dampingRatio = 0.8f,
    stiffness = 600f
)
```

**Elastic character:**
```kotlin
val animSpec = spring<Float>(
    dampingRatio = 0.5f,   // < 0.7 creates overshoot
    stiffness = 300f
)
```

**Cinematic character:**
```kotlin
val animSpec = tween<Float>(
    durationMillis = 600,
    easing = FastOutSlowInEasing
)
```

**Mechanical character:**
```kotlin
val animSpec = tween<Float>(
    durationMillis = 150,
    easing = LinearEasing
)
```

**Staggered list entries:**
```kotlin
@Composable
fun StaggeredItem(index: Int, content: @Composable () -> Unit) {
    val visible = remember { Animatable(0f) }
    val offsetY = remember { Animatable(12f) }

    LaunchedEffect(Unit) {
        delay(index * 50L)
        launch {
            visible.animateTo(1f, tween(220, easing = FastOutSlowInEasing))
        }
        launch {
            offsetY.animateTo(0f, spring(dampingRatio = 0.75f, stiffness = 400f))
        }
    }

    Box(
        modifier = Modifier
            .graphicsLayer {
                alpha = visible.value
                translationY = offsetY.value
            }
    ) { content() }
}
```

---

## Custom Pressable (Replace Default Button)

```kotlin
@Composable
fun BrandButton(
    label: String,
    onClick: () -> Unit,
    variant: ButtonVariant = ButtonVariant.Primary,
) {
    val interactionSource = remember { MutableInteractionSource() }
    val isPressed by interactionSource.collectIsPressedAsState()

    val scale by animateFloatAsState(
        targetValue = if (isPressed) 0.97f else 1f,
        animationSpec = spring(dampingRatio = 0.7f, stiffness = 800f)
    )

    val bgColor = when (variant) {
        ButtonVariant.Primary -> BrandColors.primary
        ButtonVariant.Ghost -> Color.Transparent
    }
    val textColor = when (variant) {
        ButtonVariant.Primary -> BrandColors.background
        ButtonVariant.Ghost -> BrandColors.text
    }
    val borderColor = when (variant) {
        ButtonVariant.Primary -> Color.Transparent
        ButtonVariant.Ghost -> BrandColors.primary
    }
    // Intentional: Primary = pill (999.dp), Ghost = sharp (0.dp)
    val shape = when (variant) {
        ButtonVariant.Primary -> RoundedCornerShape(999.dp)
        ButtonVariant.Ghost -> RoundedCornerShape(0.dp)
    }

    Box(
        modifier = Modifier
            .graphicsLayer { scaleX = scale; scaleY = scale }
            .clip(shape)
            .border(1.5.dp, borderColor, shape)
            .background(bgColor)
            .clickable(interactionSource = interactionSource, indication = null, onClick = onClick)
            .padding(horizontal = 28.dp, vertical = 14.dp),
        contentAlignment = Alignment.Center
    ) {
        Text(
            text = label.uppercase(),
            style = TextStyle(
                fontFamily = FragmentMono,
                fontSize = 12.sp,
                letterSpacing = 0.15.em,
                color = textColor,
            )
        )
    }
}

enum class ButtonVariant { Primary, Ghost }
```

---

## Navigation — Breaking the Default

**Avoid default `NavigationBar` with 5 items.**

```kotlin
// Custom header instead of TopAppBar
@Composable
fun BrandHeader(title: String) {
    Column(
        modifier = Modifier
            .fillMaxWidth()
            .padding(start = 24.dp, end = 24.dp, top = 16.dp),
        horizontalAlignment = Alignment.Start,
    ) {
        Text(
            text = title.uppercase(),
            style = MaterialTheme.typography.labelSmall,
            color = BrandColors.textMuted,
            letterSpacing = 2.sp,
        )
        Spacer(Modifier.height(4.dp))
        Text(
            text = title,
            style = MaterialTheme.typography.displayLarge,
            color = BrandColors.text,
        )
    }
}
```

**Replace BottomNavigation with custom tab bar:**
```kotlin
@Composable
fun AccentTabBar(
    tabs: List<String>,
    selected: Int,
    onSelect: (Int) -> Unit,
) {
    Row(
        modifier = Modifier
            .fillMaxWidth()
            .padding(horizontal = 24.dp)
    ) {
        tabs.forEachIndexed { i, tab ->
            Column(
                modifier = Modifier
                    .weight(1f)
                    .clickable { onSelect(i) },
                horizontalAlignment = Alignment.CenterHorizontally,
            ) {
                Text(
                    text = tab.uppercase(),
                    style = MaterialTheme.typography.labelSmall,
                    color = if (i == selected) BrandColors.text else BrandColors.textMuted,
                )
                Spacer(Modifier.height(6.dp))
                Box(
                    modifier = Modifier
                        .height(1.5.dp)
                        .fillMaxWidth(0.6f)
                        .background(
                            if (i == selected) BrandColors.accent else Color.Transparent
                        )
                    // No animation on the line — instant, physical
                )
            }
        }
    }
}
```

---

## Spatial Grammar — Compose

**Asymmetric padding (intentional imbalance):**
```kotlin
Modifier
    .padding(start = 32.dp, end = 20.dp, top = 24.dp, bottom = 16.dp)
```

**Not everything should be a `LazyColumn` with `Card`. Use raw layout:**
```kotlin
LazyColumn(
    modifier = Modifier
        .fillMaxSize()
        .background(BrandColors.background),
    contentPadding = PaddingValues(0.dp),
) {
    itemsIndexed(items) { index, item ->
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .padding(horizontal = 24.dp, vertical = 14.dp)
        ) {
            // Custom row content, no Card wrapper
        }
        if (index < items.lastIndex) {
            Divider(
                color = BrandColors.primary.copy(alpha = 0.2f),
                thickness = 0.5.dp,
                modifier = Modifier.padding(horizontal = 24.dp)
            )
        }
    }
}
```

---

## Common Mistakes to Avoid in Compose

| ❌ Generic | ✅ Differentiated |
|------------|------------------|
| `MaterialTheme.colorScheme.surface` | Named brand color tokens |
| `Card(shape = RoundedCornerShape(12.dp))` | Context-specific shape (0, 6, or 999) |
| `NavigationBar { NavigationBarItem(...) }` | Custom tab/nav composable |
| `Button(onClick = ...) { Text("Save") }` | Custom `ButtonStyle` with brand motion |
| `TopAppBar(title = { Text("...") })` | Custom header composable with brand type |
| `spring()` with no parameters | Explicit `dampingRatio` + `stiffness` |
| `.padding(16.dp)` everywhere | Asymmetric, intentional spacing |
| Default Material3 colors | `BrandColors` object with 5+ tokens |
