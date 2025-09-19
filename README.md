# Aseprite Build — using GitHub Action
### Cloud-Powered Aseprite Builds for Windows via GitHub Actions

> **To Aseprite lovers!**

If you truly love Aseprite, please support the creator! (https://www.aseprite.org/)

**However, for those who cannot afford to pay, this is a way to build Aseprite yourself.**

This guide provides instructions to build Aseprite specifically for Windows using GitHub Actions.

## Prerequisites

- A GitHub account
- Basic familiarity with GitHub workflows

## Quick Setup

1. Get the **build-windows-dp.yaml** from [here](https://github.com/MengheangHeak/aseprite-cloud-built/blob/main/.github/workflows/build-windows-dp.yml)

2. Create a new repository on GitHub

3. In your repository, create a new workflow:
   - Go to "Actions" → "New workflow"
   - Choose "Set up a workflow yourself" (skip the template selection)
   - Copy and paste the code from **build-windows-dp.yaml** into your new YAML file
   - Commit the workflow file

4. The workflow will automatically run on push to the main branch, or you can manually trigger it from the Actions tab

## Downloading the Built Application

After the workflow completes successfully:

1. Go to the "Actions" tab in your repository
2. Click on the latest workflow run
3. Scroll down to the "Artifacts" section
4. Download the `aseprite-windows` artifact which contains the built executable

## Installation Notes

1. **Alternative Output Path**: By default, the workflow uploads files from `build/bin`. You might want to change this to use the installation directory instead:
   ```yaml
   - name: Upload Artifact
     uses: actions/upload-artifact@v4
     with:
       name: aseprite-windows
       path: dist  # Changed from build/bin
   ```

2. **File Organization**: After downloading, you must copy the `.exe` file from the `/bin` folder to the `/share` folder to be able to execute the application properly, as the application data is located in the `/share` folder.

3. **Dependency Issue**: If you encounter an error that `libcrypto-3-x64.dll` was not found, you can download it from: https://www.dll-files.com/libcrypto-3-x64.dll.html and place it in the same directory as the Aseprite executable.

## Version Considerations

⚠️ **Important**: The default workflow uses specific versions:
- Aseprite v1.3.15.2
- Skia m124-08a5439a6b

If you need a different version, you must modify these URLs in the workflow:

```yaml
# For Aseprite source (change the version number):
Invoke-WebRequest -Uri "https://github.com/aseprite/aseprite/releases/download/v1.3.15.2/Aseprite-v1.3.15.2-Source.zip" -OutFile $sourceZip

# For Skia (check available releases):
Invoke-WebRequest -Uri "https://github.com/aseprite/skia/releases/download/m124-08a5439a6b/skia-windows-Release-x64.zip" -OutFile $skiaZip
```

Check these repositories for available versions:
- Aseprite releases: https://github.com/aseprite/aseprite/releases
- Skia releases: https://github.com/aseprite/skia/releases


## Notes

- This process may take 15-30 minutes to complete


## Resources

- Aseprite Official Repository: https://github.com/aseprite/aseprite
- Aseprite Official Website: https://www.aseprite.org/

---

*This guide is provided for educational purposes. Please support the Aseprite developers if you can afford to do so.*
