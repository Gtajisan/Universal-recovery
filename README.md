# Recovery Builder for |TWRP / PBRP / OFRP / SHRP|
Compile your first custom recovery via Github Actions.

This repo comes from a long chain of forks and finally ended up with working shrp and some revamping of the workflow files to work for older android devices (tested with 9.0). 

It uses github noreply account (if u dont know what that is, read the last section in notes).

If there are any issues relating the build tree info (not the workflow file config entries), feel free to open a pull request.

## How to Use
1. Fork this repository.

2. Ensure GitHub Actions are enabled on your fork (Repository Settings > Actions > General > Allow all actions).

3. Create or locate your device tree repository and branch (for example: `https://github.com/you/android_device_vendor_device` with branch `android-11`).

4. Open the `Actions` tab on your fork and select the workflow that matches your target recovery:
   - **TeamWin [TWRP]** for modern TWRP builds.
   - **TWRP (android 4.4+)** only if you are targeting KitKat-era sources.
   - **PitchBlack [PBRP]** for PitchBlack Recovery.
   - **OrangeFox [OFRP]** for OrangeFox Recovery.
   - **SkyHawk [SHRP]** for SkyHawk Recovery.

5. Click **Run workflow** and fill in the inputs:
   - **Manifest Branch**: pick the Android branch (12.1, 11, 10, 9, 8.1, 7.1, 6.0, or 4.4 for legacy TWRP).
   - **Device Tree**: the full HTTPS URL for your device tree repo.
   - **Device Tree Branch**: the branch name that matches your manifest branch.
   - **Build Target**: `boot`, `recovery`, or `vendorboot` based on your device.

6. Wait for the job to finish, then download artifacts from the workflow run summary or check GitHub Releases if the workflow uploads there.

## Setup Checklist
- **Make sure your device tree matches the manifest branch.** A mismatch is the most common reason for sync or build errors.
- **Verify your device tree path layout.** The workflows expect a standard Android device tree layout under `device/<vendor>/<device>`.
- **Confirm the build target.** Modern devices may require `vendorboot` instead of `boot` or `recovery`.
- **For legacy TWRP (4.4)**: use the dedicated workflow and ensure your device tree is compatible with older build systems.

## Inputs Reference
| Input | Description | Example |
| --- | --- | --- |
| Manifest Branch | Android manifest branch to sync. | `12.1` |
| Device Tree | HTTPS URL for the device tree repository. | `https://github.com/you/android_device_vendor_device` |
| Device Tree Branch | Branch name in your device tree repo. | `android-12.1` |
| Build Target | Image to build. | `recovery` |


## About LDCHECK

  You can use LDCHECK to get info about dependencies or drivers that are missing for encryption, and help in looking for the drivers which would be needed from your root folders. 
  You can check out the wiki (Currently WIP, planning to BoardConfig flags based on manifest-branch, ways to debug (like finding .xml files), ) where you can add a path to a LDCHECK file,, as well as your device, processor info (might make it more specific later)

 - LDCHECK (path to your target binary file, ie. `system/bin/qseecomd`)
   - If you are building manually/locally and you want to use ldcheck for checking dependencies, visit [THIS](https://github.com/TeamWin/android_device_qcom_twrp-common/tree/android-11#using-ldcheck-to-find-dependencies) for guide.

## Notes

- If you created your account on GitHub.com after July 18, 2017, your noreply email address for GitHub is an ID number and your username in the form of ID+USERNAME@users.noreply.github.com. If you created your account on GitHub.com prior to July 18, 2017, and enabled `Keep my email address private` prior to that date, your noreply email address from GitHub is USERNAME@users.noreply.github.com. You can get an ID-based noreply email address for GitHub by selecting (or deselecting and reselecting) Keep my email address private in your email settings.
- Advanced users (check [this workflow](https://github.com/mlm-games/ofox_m31s/blob/main/.github/workflows/recovery-build.yml) for tests in the repo)
- If a workflow is stuck on "Waiting for a runner to pick up this job", make sure your fork is using a supported runner label (this repo defaults to `ubuntu-latest`) and that GitHub Actions are enabled for the repository.

### Old notes ( Not relevant anymore )

> - Some of PBRP's branches have missing pb_build.sh files (like 9.0), so the build will fail, but you can still flash the recovery.img and it will be uploaded to releases. For the .zips, you can go to PBRP's vendor utils repo and find them there in PBRP/tools (location might wary).
> - Why ubuntu-20.04 for some workflows? Because python-is-python2 is replaced with python-is-python3 past 20.04.


## Thanks/Credits
 - [CaptainThrowback](https://github.com/CaptainThrowback)
 - [azwhikaru](https://github.com/azwhikaru)
 - [cd-Crypton](https://github.com/cd-Crypton)
 - [that1](https://github.com/that1)
 - [carlodandan](https://github.com/carlodandan)
 - And to all Contributors in every repositories and scripts I used.
 - [Recovery builder (derived from) and lazycodebuilder](https://github.com/lazycodebuilder/Lazy_Action-Recoverys-Builder)
 - [ZH-XiJun](https://github.com/ZH-XiJun) - android 4.4 support
