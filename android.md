https://geckoview.dev

Run the android emulator:

`mach android-emulator`

Android Products:
  * Firefox Preview - Soon to be Firefox Fenix?
  * Firefox Focus

Platform: GeckoView
 * XUL was used to build Fennec. Intermingled XUL, front-end and the platform.
 * XUL was really bad for performane.
 * Switched to Fennec being built on Android technology, with it interfacing with the platform.

Switch to:
 * App <-> GeckoView <-> Platform
 * https://searchfox.org/mozilla-central/source/mobile/android/chrome/geckoview/geckoview.js

Android Components:
 * Front-end abstraction to avoid forking the mobile browser

 GeckoView Architecture:
  * Key classes
    * GeckoRuntime
      - XRE_Main (parent)
      - Starts Gecko
      - Prefs
      - Command line arguments
      - Global configuration (e.g. Telemetry)
    * GeckoSession
      - <browser>
      - Conceptually a tab
      - Handle navigation
      - Interface between App and Web platform
    * GeckoView
      - Native widget
      - forwards input to GeckoSession
      - Displays compositor surface

GeckoRuntime is long running, and controls all things. It can spin up GeckoSession and GeckoView. GeckoView is a true view layer.

Android Studio - Industry standard for working with Android
 - Do not accept any upgrades
 - Disable Instant Run
 - Select build Variant withGeckoBinariesDebug
 - Select "geckoview_exmaple"

adb logcat
  - Android Device Bridge
  - use this for logging, printf_debug
