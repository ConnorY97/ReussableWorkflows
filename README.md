# Godot Build Action

This GitHub Action automates the process of building a Godot project for Windows Desktop using a specified version of Godot and export templates.

## Inputs

| Input Name      | Description                                                        | Default           | Required |
| --------------- | ------------------------------------------------------------------ | ----------------- | -------- |
| `godot_version` | The version of Godot to use (e.g., `4.6`).                         | `4.6`             | Yes      |
| `export_preset` | The export preset to use (e.g., `Windows Desktop`).                | `Windows Desktop` | Yes      |
| `export_dir`    | The directory to store the exported files (e.g., `build/windows`). | `build/windows`   | Yes      |
| `export_exe`    | The name of the exported executable (e.g., `FMOD-Test.exe`).       | `FMOD-Test.exe`   | Yes      |

## Example Workflow

You can use this action in your GitHub workflows like this:

```yaml
name: Build Godot Project

on:
  push:
    branches: [build]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Build Godot Project using composite action
        uses: ./godot-build-action
        with:
          godot_version: '4.6'
          export_preset: 'Windows Desktop'
          export_dir: 'build/windows'
          export_exe: 'FMOD-Test.exe'
```

### Inputs Explanation

* **`godot_version`**: The version of Godot to use for building the project. This is a required input. Example: `4.6`.

* **`export_preset`**: The export preset defines the platform you are exporting for. For example, if you want a Windows Desktop build, use `Windows Desktop`.

* **`export_dir`**: This specifies the directory where the exported build will be placed. The default is `build/windows`, but you can customize it as needed.

* **`export_exe`**: This specifies the name of the output executable file. By default, it’s set to `FMOD-Test.exe`, but you can change this to any name that suits your project.

## How It Works

1. **Dependencies**: Installs `unzip` and `wget` to handle downloading and extracting files.

2. **Godot Setup**:

   * Downloads the specified version of Godot.
   * Extracts and makes it executable.

3. **Export Templates**:

   * Downloads the export templates required for building.
   * Corrects the folder structure for Windows exports.

4. **Build**:

   * Uses Godot's command line interface to export the project using the provided export preset.
   * The exported file is saved to the specified directory.

5. **Artifact Upload**:

   * Uploads the built executable as an artifact for further use in the workflow.

## Requirements

* This action runs on `ubuntu-latest`, so it will work on GitHub-hosted runners using the Ubuntu operating system.
* You must have a Godot project in your repository for the export process to work.

## License

This action is open-source and available under the MIT License.

---

You can further modify this README depending on any additional requirements or details. Feel free to ask if you'd like any changes or additions!
