# gdrive-appdata

Tries to fetch the contents of the [appdata](https://developers.google.com/drive/v3/web/appdata) hidden folder from Google Drive.

Helps identify what Android applications might be saving/backing up on Google Drive.

## Requirements
 * Python 3
 * Google Drive Python client library
   * details: [Python Quickstart](https://developers.google.com/drive/v3/web/quickstart/python)
```
pip install -r requirements.txt
```

## Usage

Requires Google account and password. Creating an app-specific password instead of using the raw password is recommended (especially when two-step verification is turned on). If got `Error: Need Broswer`, please follow this [link](https://accounts.google.com/b/0/DisplayUnlockCaptcha).

Specify either a package name and signature (SHA-1 hash of the raw signing certificate), or a `packages.xml` file (extracted from device). 

Device ID is optional but recommended, should be either `ANDROID_ID` or GMS device ID.

When using `packages.xml` will try to fetch data from all packages (including internal/system ones).
This can be time consuming and run into rate limiting. Use with care. You can use a combination 
of `--packages-xml` and `--target-package` to target a specific package.

Downloaded files will be saved in the current directory under:

```
appdata-<account name>-<timestamp>/<package name>/
```

## Example

```
./get-gdrive-appdata.py --account foo.bar.baz@gmail.com  --password foo.bar.baz \
--target-package com.example.app --target-package-sig 0000000000000000000000000000000000000000 \
--device-id 000000000000
```

## References, etc
 * [How can I see hidden app data in Google Drive?](https://stackoverflow.com/questions/22832104/how-can-i-see-hidden-app-data-in-google-drive/36487545#36487545)
 * [Inside the Android Play Service's magic OAuth flow](https://sbktech.blogspot.jp/2014/01/inside-android-play-services-magic.html)
 * [YuriCosta/WhatsApp-GD-Extractor-Multithread](https://github.com/YuriCosta/WhatsApp-GD-Extractor-Multithread)