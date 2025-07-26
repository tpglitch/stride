# 🏃‍♂️ Stride

Robust, flexible, and multi-format configuration-driven ZIP + file extractor built for pipelines, scripting, and offline workflows.

<p align="center">
<!--   <strong>Version</strong>: 3.7.1  
  <br> -->
  <strong>Formats</strong>: YAML • JSON • TOML • XML  
</p>

---

## 🚀 What is Stride?

Stride is a command-line tool that lets you define complex file extraction workflows via configuration files. Whether you're managing project bootstraps, deployment assets, or ZIP-based delivery pipelines, Stride gives you fine-grained control over what to download, extract, rename, and ignore across multiple formats.

---

## 🔧 Features

* 📦 Extract multiple ZIP archives with precise filtering
* 📁 Pre-create folder structures for your pipeline
* 🔗 Download single files and rename them as needed
* ✍️ Fully declarative configs in YAML, JSON, TOML, or XML
* 🔎 Fine-grained include/exclude filtering: filenames, globs, directories
* 🧠 Format auto-detection + manual override
* 🛡 Built-in validation to prevent rule conflicts
* 🗂 Flatten or preserve folder structures
* 🌐 Remote config support via HTTP(S) URLs

---

## 📑 Supported Formats

Stride config files can be written in:

| Format | Extension(s)    |
| ------ | --------------- |
| YAML   | `.yaml`, `.yml` |
| JSON   | `.json`         |
| TOML   | `.toml`         |
| XML    | `.xml`          |

Auto-detection is based on file extension, or use:

```bash
--override-type-detection=yaml|json|toml|xml
```

---

## ⚙️ CLI Usage

```bash
# Get version
stride --version

# Get version (shorter)
stride -V

# Basic usage (auto-detect format)
stride extract -c config.yaml

# Override format
stride extract -c config.conf --override-type-detection=toml

# Set output directory
stride extract -c config.yaml -o build

# Remote config file
stride extract -c https://example.com/myconfig.yml

# Enable verbose logging for debugging
stride extract -c config.yaml -v
```

---

## 🛠 Debugging Tips

* Use -v / --verbose to see exactly what gets filtered and why.
* Use --override-type-detection when file extensions are ambiguous.
* Validate config structure with:

  * `yamllint`, `jsonlint`, `toml-validator`, `xmllint`

---

## 💡 Best Practices

* Stick to one format per project (YAML is most readable)
* Use descriptive `name` fields for traceable logs
* Combine filtering rules for precision
* Use `strip_root_folder` when pulling GitHub archives
* Always validate before deploying

---

## 📘 Example Project

```yaml
output_structure:
  "#/logs": { description: "Runtime logs", create: true }
  "#/temp": { description: "Temp files", create: true }

zip_sources:
  - url: "https://nodejs.org/dist/v18.14.0/node-v18.14.0-win-x64.zip"
    name: "NodeJS v18.14.0"
    target_dir: "#/bin"
    include_directories: ["bin", "lib"]
    exclude_directories: ["share/doc"]
    include_patterns: ["*.exe", "*.dll"]
    preserve_structure: false

file_sources:
  - url: "https://example.com/app/config.json"
    name: "App Config"
    target_path: "#/conf"
    rename_to: "app-config.json"
```

---

## 🧭 License & Contribution

Stride is proprietary software, and not accepting pull requests. We accept issues and feature requests!

---

Happy automating!
