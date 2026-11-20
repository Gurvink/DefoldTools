# Build Manager

The Build Manager provides a consistent way to configure and start Defold builds. It keeps build-related settings and steps in one place so that local builds and automated workflow builds use the same process. the [Build Manager](build_manager.editor_script) and [Custom Bundle Patcher](custom_bundle_patcher.lua) are suppose to be placed in the tools folder inside a Defold project.

## Typical workflow

1. **Open Build Manager** - Open the manager in project -> Build Manager
2. **Configure the settings** - select the platforms that are to be included in the build and configure the paths for different config files.
3. **Configure each platform** - select the settings for each of the different platforms.
4. **Start the builds** - Each build will startwith the selected settings and be placed into the folders that are selected (standard is /build)

## Workflow usage

The workflow automates the same steps used locally:

1. Check out the repository.
2. Read the build.json file to get the settings
3. Apply the settings for each platform that gets built
4. Build each platform
5. The builds are available in the artifacts of the run


## Settings

### Global Settings

These settings apply globally to the game and build configuration.

| Setting | Key | Type | Default | Description |
|---|---|---|---|---|
| Game Version | `version` | Text | `0.0.0` | The version of the game, used for live updates and other purposes. |
| Platform Path | `platform_path` | File | `_services/platform.lua` | Path to the platform.lua file, used for platform-specific code. |
| Game Manager Path | `gamemanager_path` | File | `_modules/gamemanager.lua` | Path to the gamemanager.lua file, used for game management. |
| Config Path | `config_path` | File | `_services/config.lua` | Path to the config.lua file, used for configuration. |
| AB Tester Path | `ab_tester_path` | File | `_modules/A_B_tester.lua` | Path to the A/B tester file, used for A/B testing. |
| Custom API Path | `custom_api_path` | File | `_modules/API/custom_API.lua` | Path to the custom API file, used for custom API calls. |
| Game Project Path | `game_project_path` | File | `game.project` | Path to the game project file, used for building the game. |

All file paths in this section are relative.

### Bundle Settings

These settings control application-specific features and configuration.

| Setting | Key | Type | Default | Options | Description |
|---|---|---|---|---|---|
| App Type | `app_type` | Select | `default` | `default`, `curator`, `viewer` | Application type used for platform-specific code. |
| Debug | `debug` | Checkbox | `false` | `true`, `false` | Enables debug mode, including debug symbols and other debug features. |
| AB Testing | `ab_testing` | Checkbox | `false` | `true`, `false` | Enables A/B testing for different versions of the game. |
| Force Version | `force_version` | Checkbox | `false` | `true`, `false` | Forces a specific game version for A/B testing. |
| Forced Version | `forced_version` | Select | `default` | `default` | Specifies the version to force during A/B testing. |
| Force Creation | `force_creation` | Checkbox | `false` | `true`, `false` | Forces the creation of a new A/B testing group. |
| Amplitude | `amplitude` | Checkbox | `false` | `true`, `false` | Enables Amplitude analytics to track user behavior. |
| Region Lock | `region_lock` | Checkbox | `false` | `true`, `false` | Restricts Amplitude to America and Georgia. |

### Common Build Settings

These settings apply to builds across all supported platforms.

| Setting | Key | Type | Default | Options | Description |
|---|---|---|---|---|---|
| Variant | `variant` | Select | `debug` | `debug`, `release`, `headless` | Engine variant used for the build. |
| Texture Compression | `texture_compression` | Checkbox | `false` | `true`, `false` | Enables texture compression for the build. |
| Generate Debug Symbols | `with_symbols` | Checkbox | `false` | `true`, `false` | Generates debug symbols for debugging crashes and other issues. |
| Generate Build Report | `build_report` | Checkbox | `false` | `true`, `false` | Generates a report to analyze build size and other metrics. |
| Publish Live Update Content | `liveupdate` | Checkbox | `false` | `true`, `false` | Publishes live update content to update the game without a full rebuild. |
| Contentless Bundle | `contentless` | Checkbox | `false` | `true`, `false` | Creates a bundle without content. |
| Output Path | `output` | Directory | `builds` | Custom directory | Directory where the build output is stored. |

The output directory is configured as a non-relative path setting.

## Platform Settings

Platform-specific settings are available depending on the selected build target.

### Windows

| Setting | Key | Type | Default | Options | Description |
|---|---|---|---|---|---|
| Platform | `platform` | Select | `x86_64_win32` | `x86_64_win32` | Target platform for Windows builds. |

### Linux

| Setting | Key | Type | Default | Options | Description |
|---|---|---|---|---|---|
| Platform | `platform` | Select | `x86_64-linux` | `x86_64-linux`, `arm64-linux` | Target architecture. x86_64 supports Intel/AMD processors, while arm64 supports ARM processors. |

### macOS

| Setting | Key | Type | Default | Options | Description |
|---|---|---|---|---|---|
| Architectures | `architectures` | Multiselect | `x86_64-macos`, `arm64-macos` | `x86_64-macos`, `arm64-macos` | Target architectures. x86_64 supports Intel-based Macs, while arm64 supports Apple Silicon. |

### Android

| Setting | Key | Type | Default | Options | Description |
|---|---|---|---|---|---|
| Architectures | `architectures` | Multiselect | `arm64-android` | `arm64-android`, `armv7-android`, `x86_64-android` | Target architectures for Android builds. |
| Bundle Format | `bundle_format` | Multiselect | `apk` | `apk`, `aab` | Output format. APK is used for Android devices, while AAB is used for Google Play Store distribution. |
| Keystore | `keystore` | File | Empty | File path | Keystore file used to sign the Android build. |
| Keystore Password File | `keystore_pass` | File | Empty | File path | Password file for the Android keystore. |
| Key Password File | `key_pass` | File | Empty | File path | Password file for the signing key. |
| Install on Connected Device | `install` | Checkbox | `false` | `true`, `false` | Installs the build on a connected Android device after building. |
| Launch Installed App | `launch` | Checkbox | `false` | `true`, `false` | Launches the installed application on a connected Android device after building. |

### HTML5

| Setting | Key | Type | Default | Options | Description |
|---|---|---|---|---|---|
| Architectures | `architectures` | Multiselect | `wasm-web` | `wasm-web`, `wasm_pthread-web` | Target WebAssembly architecture. wasm_pthread-web enables WebAssembly with pthread support. |

### iOS

| Setting | Key | Type | Default | Options | Description |
|---|---|---|---|---|---|
| Sign Application | `sign` | Checkbox | `false` | `true`, `false` | Signs the application using a provisioning profile and code signing identity. |
| Code Signing Identity | `code_signing_identity` | Select | `iPhone Developer` | `iPhone Developer`, `iPhone Distribution` | Code signing identity used for signing the iOS build. |
| Provisioning Profile | `provisioning_profile` | File | Empty | File path | Provisioning profile used for signing the iOS build. |
| Architectures | `architectures` | Multiselect | `arm64-ios` | `arm64-ios` | Target architecture for iOS builds. |
| Install on Connected Device | `install` | Checkbox | `false` | `true`, `false` | Installs the build on a connected iOS device after building. |
| Launch Installed App | `launch` | Checkbox | `false` | `true`, `false` | Launches the installed application on a connected iOS device after building. |
