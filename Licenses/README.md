# Bundled runtime notices

MakerBridge 1.1.7 Beta is developed by Brian Mayes. Feedback: brian_mayes@me.com.

The Mac app includes CPython 3.13.16 and the required standard-library modules, packaged for Apple silicon using PyInstaller 6.22.3. The runtime was obtained from the Python Software Foundation's official macOS installer:

https://www.python.org/ftp/python/3.13.16/python-3.13.16-macos11.pkg

Installer SHA-256: `30666509020b4da0dd8bc2e773255f34d76b7bb80b66960a928d5f6daa0192d7`.

Python's license is reproduced in `Python-LICENSE.txt`. `Python-third-party-licenses.html` reproduces the third-party notices from the Python 3.13.16 documentation. The runtime includes OpenSSL 3.5.9; its license is in `OpenSSL-LICENSE.txt`. Packaging relocates library references and includes the arm64 portions needed by this app.

PyInstaller's bootloader distribution exception is documented at https://pyinstaller.org/en/stable/license.html.

Snapmaker Orca and Bambu Studio are separate installations. Their printer profiles are read locally and are not bundled or relicensed by MakerBridge. The Python installer's publisher signature and notarization do not confer Apple notarization on MakerBridge.

The Windows build bundles its own Python runtime, Tcl/Tk and OpenSSL. Exact versions and Windows-specific notices are recorded in `WINDOWS.md` inside each Windows download.
