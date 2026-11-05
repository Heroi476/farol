npx expo install expo-glass-effect
import { Pressable, Text, StyleSheet, Platform } from "react-native";
import { GlassView, isLiquidGlassAvailable } from "expo-glass-effect";

export function GlassButton({ title, onPress }: { title: string; onPress: () => void }) {
  const hasGlass = Platform.OS === "ios" && isLiquidGlassAvailable();

  return (
    <Pressable onPress={onPress}>
      <GlassView
        glassEffectStyle="regular"
        isInteractive
        style={[styles.button, !hasGlass && styles.fallback]}
      >
        <Text style={styles.text}>{title}</Text>
      </GlassView>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  button: { paddingVertical: 14, paddingHorizontal: 24, borderRadius: 999, alignItems: "center" },
  fallback: { backgroundColor: "rgba(255,255,255,0.15)" },
  text: { color: "#fff", fontWeight: "600" },
});
