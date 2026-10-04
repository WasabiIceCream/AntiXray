# Gameoverse build of Anti-Xray

Fork of [DrexHD/FabricAntiXray](https://github.com/DrexHD/FabricAntiXray) (MIT) at tag `fabric-1.4.16+26.1`, branch
`gameoverse-26.1.2`, built for the Gameoverse server (Fabric 26.1.2).

## Change

Three scoped-value reads in the chunk write path (`PalettedContainerMixin`, `PalettedContainer$DataMixin`) are
guarded with `isBound()`. A biome resend (`/fillbiome`, or Aerial Hell's biome corruption) writes chunk data outside
the scope that binds those values, and the unguarded `get()` crashed the server. Don't use `ScopedValue.orElse(null)`
for this: it throws on a null default.

## Building

`JAVA_HOME=/usr/lib/jvm/java-25-openjdk sh ./gradlew :fabric:build`; the jar is
`fabric/build/libs/antixray-fabric-1.4.16-gameoverse.1+26.1.jar`.
