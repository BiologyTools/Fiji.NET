# Fiji.NET (IKVM-based Fiji + Bio-Formats for .NET 10)

## Overview

**Fiji.NET** provides a way to run Fiji (ImageJ distribution) and Bio-Formats inside a .NET application using IKVM. It enables loading, processing, and converting microscopy images directly from C# without requiring a separate Java runtime environment at execution time.

This project bridges the Java-based imaging ecosystem (ImageJ/Fiji/Bio-Formats) with modern .NET applications such as BioGTK, BioImager, and other microscopy workflows.

---

## ⚠️ Important Compatibility Note

This project is based on the **last Java 8–compatible Fiji stack**.

Implications:

* Uses legacy ImageJ + SciJava ecosystem versions
* Newer Fiji / ImageJ2 features (Java 11+) are **not available**
* Some plugins may not function under IKVM
* SciJava command discovery is **partially limited**

This tradeoff is required because IKVM targets Java 8 bytecode compatibility.

---

## Key Features

* Run Fiji/ImageJ inside .NET via IKVM
* Load microscopy formats using Bio-Formats
* Access `ImagePlus` objects directly in C#
* Support for hundreds of scientific image formats (NDPI, OME-TIFF, CZI, etc.)
* No external Fiji installation required at runtime
* Targeted for **.NET 10**
* **Simple installation via NuGet**

---

## Installation (NuGet)

The recommended way to use Fiji.NET is via NuGet:

```bash id="1wq3p6"
dotnet add package Fiji.NET
```

This automatically includes:

* Required Fiji / ImageJ jars
* SciJava dependencies
* Bio-Formats (`bioformats_package.jar`)
* IKVM configuration

No manual jar management is required.

---

## Architecture

```text id="q2e5r9"
.NET 10 (C#)
   ↓
IKVM Runtime
   ↓
Fiji / ImageJ (Java 8)
   ↓
Bio-Formats
   ↓
Microscopy Images
```

---

## Usage

### Initialize ImageJ (optional UI)

```csharp id="d7zq8k"
ij.ImageJ ijm = new ij.ImageJ();
```

---

### Load an image using Bio-Formats

```csharp id="m9xk2v"
ij.ImagePlus[] imps = loci.plugins.BF.openImagePlus("test.ome.tif");
ij.ImagePlus imp = imps[0];
```

---

### Access pixel data

```csharp id="v3n6yb"
var processor = imp.getProcessor();
int width = imp.getWidth();
int height = imp.getHeight();
```

---

## Notes

* Bio-Formats is used directly via API (`loci.plugins.BF`)
* Fiji is embedded and does not require a separate installation
* Designed for programmatic use rather than full plugin-driven workflows

---

## Recommended Strategy

For stability:

* Use the NuGet package (avoid manual jar setup)
* Use Bio-Formats API directly

---

## Summary

Fiji.NET enables:

* Reliable microscopy image loading in .NET 10
* Seamless access to Bio-Formats
* Integration with modern .NET imaging tools

Best practice:

> Use Bio-Formats as a library, not as a plugin system, when running under IKVM.

---

## Credits

* ImageJ / Fiji
* Bio-Formats (OME)
* SciJava ecosystem
* IKVM

