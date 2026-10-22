# Standalone registry release

Build the Sputnik SDK first, then bind its exact native SDK and runtime:

```sh
export SPUTNIK_ROOT=/path/to/sputnik-lang
python3 release/providers.py --sdk "$SPUTNIK_ROOT"
python3 release/prepare.py build/release-config.json --native source --modules source
python3 release/prepare.py build/release-config.json --native prebuilt --modules source
```

The current verified target is macOS arm64 (macOS 26+). `bytecode` and `mixed`
module delivery are also supported. All native variants declare exact runtime
version, ABI and build hashes. Source variants additionally require the matching
SDK headers. Set `SPUTNIK_NATIVE_PROVIDERS` to the runtime and SDK directories
printed by the provider script before installing or compiling consumers.
These provider assets are local inputs and are not uploaded with the package.
The distribution uses the `slowpilot.sdk.*` module namespace.
