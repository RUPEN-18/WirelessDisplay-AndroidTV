ANDROID TV RECEIVER — FINAL FIXED PACKAGE

The two red errors:
- Unresolved reference 'lt_logo_full'
- Unresolved reference 'lt_symbol'

are caused by missing Android drawable resources in the project where MainActivity.kt was pasted.

This package already contains the required files at:
app/src/main/res/drawable-nodpi/lt_logo_full.png
app/src/main/res/drawable-nodpi/lt_symbol.png

IMPORTANT:
- Keep MainActivity.kt exactly where it is:
  app/src/main/java/com/wirelessdisplay/receiver/MainActivity.kt
- Keep both PNG files inside drawable-nodpi.
- Open this folder as the Android Studio project OR copy the complete app/src/main folder
  into your existing AndroidTVReceiver project.

After copying:
1. Android Studio -> File -> Sync Project with Gradle Files
2. Build -> Clean Project
3. Build -> Rebuild Project

The remaining messages such as:
"Property white is never used"
"String literal in setText can not be translated"
"Parameter e is never used"
etc. are LINT/inspection warnings, not compile errors.

The TV UI and streaming logic are unchanged.
