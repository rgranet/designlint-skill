# React Native Reference

## React Native Convergence Traps

- `StyleSheet.create` with hardcoded colors everywhere
- Default `TouchableOpacity` with `activeOpacity={0.7}`
- `FlatList` with no custom separator or item styling
- `View` + `Text` with no token system
- Animations limited to `Animated.timing` with `duration: 300`

---

## Token System

```ts
// theme.ts
export const theme = {
  colors: {
    bg:          '#1C1917',
    surface:     '#292524',
    primary:     '#D97706',
    accent:      '#FCD34D',
    text:        '#E7E5E4',
    textMuted:   '#A8A29E',
  },
  fonts: {
    display:  'PlayfairDisplay-Bold',
    body:     'SourceSerif4-Light',
    mono:     'FragmentMono-Regular',
  },
  fontSizes: {
    displayXL: 44,
    displayLG: 32,
    headingMD: 22,
    body:      17,
    label:     11,
    caption:   14,
  },
  space: {
    xs:  6,
    sm:  14,
    md:  28,
    lg:  56,
    xl:  112,
  },
  motion: {
    fast:   150,
    base:   220,
    slow:   500,
  }
}
```

---

## Reanimated 2 — Motion Patterns

**Snappy spring (default for interactions):**
```tsx
const style = useAnimatedStyle(() => ({
  transform: [{ scale: withSpring(pressed.value ? 0.97 : 1, {
    damping: 15,
    stiffness: 300,
  })}]
}))
```

**Staggered list entries:**
```tsx
function AnimatedRow({ item, index }: Props) {
  const opacity = useSharedValue(0)
  const translateY = useSharedValue(10)
  
  useEffect(() => {
    const delay = index * 50
    opacity.value = withDelay(delay, withTiming(1, { duration: 220 }))
    translateY.value = withDelay(delay, withSpring(0, { damping: 20, stiffness: 200 }))
  }, [])
  
  const style = useAnimatedStyle(() => ({
    opacity: opacity.value,
    transform: [{ translateY: translateY.value }]
  }))
  
  return <Animated.View style={[styles.row, style]}>{/* ... */}</Animated.View>
}
```

---

## Custom Pressable (replace TouchableOpacity)

```tsx
function BrandButton({ label, onPress, variant = 'primary' }: Props) {
  const pressed = useSharedValue(0)
  
  const animStyle = useAnimatedStyle(() => ({
    transform: [{ scale: interpolate(pressed.value, [0, 1], [1, 0.97]) }],
    opacity: interpolate(pressed.value, [0, 1], [1, 0.85]),
  }))
  
  const variants = {
    primary: {
      background: theme.colors.primary,
      text: theme.colors.bg,
      border: 'transparent',
    },
    ghost: {
      background: 'transparent',
      text: theme.colors.text,
      border: theme.colors.primary,
    },
  }
  
  const v = variants[variant]
  
  return (
    <Pressable
      onPressIn={() => { pressed.value = withTiming(1, { duration: 80 }) }}
      onPressOut={() => { pressed.value = withSpring(0, { damping: 15 }) }}
      onPress={onPress}
    >
      <Animated.View style={[{
        paddingVertical: 14,
        paddingHorizontal: 28,
        backgroundColor: v.background,
        borderWidth: 1.5,
        borderColor: v.border,
        // Intentional: no borderRadius, or extreme (999) — never "medium"
        borderRadius: variant === 'ghost' ? 0 : 999,
      }, animStyle]}>
        <Text style={{
          fontFamily: theme.fonts.mono,
          fontSize: 12,
          letterSpacing: 1.5,
          textTransform: 'uppercase',
          color: v.text,
          textAlign: 'center',
        }}>
          {label}
        </Text>
      </Animated.View>
    </Pressable>
  )
}
```
