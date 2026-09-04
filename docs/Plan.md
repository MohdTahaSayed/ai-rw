# LLM-Based Windows Malware Analysis: Fine-Tuning, RLHF and GRPO Pipeline

## 1. Project Objective

The objective of this project is to develop and evaluate Large Language Model (LLM)-based systems for static Windows malware family classification and evidence-grounded malware analysis.

The project uses a unified dataset constructed from four Windows PE malware feature sources:

- API Functions
- DLL Imports
- PE Header
- PE Sections

The final dataset contains 29,489 malware samples represented by 318 selected static features.

Three foundation models will be investigated:

1. DeepSeek-Coder
2. Qwen2.5-Coder-1.5B-Instruct
3. Llama-3.2-3B-Instruct

The models will be adapted using parameter-efficient fine-tuning, primarily QLoRA, followed by reinforcement-learning-based approaches using RLHF and GRPO.

The overall objective is to determine whether compact, parameter-efficiently adapted foundation models can perform useful static malware-family classification and produce evidence-grounded analysis from structured PE characteristics.

---

# 2. Final Malware Dataset

The master dataset is:

`Windows_Malware_Final_318_Features.csv`

The dataset contains:

- 29,489 samples
- 318 ML features
- 1 SHA256 identifier
- 1 target variable (`Type`)
- 320 total columns

The SHA256 value uniquely identifies each malware sample and is retained for dataset traceability and leakage checking, but is not used as a predictive feature.

---

# 3. Malware Classes

The target variable contains seven classes.

| Type | Malware Class |
|---:|---|
| 0 | Benign |
| 1 | RedLineStealer |
| 2 | Downloader |
| 3 | RAT (Remote Access Trojan) |
| 4 | Banking Trojan |
| 5 | SnakeKeyLogger |
| 6 | Spyware |

The task is therefore a seven-class static malware-family classification problem.

The model receives static characteristics extracted from a Windows PE executable and predicts the corresponding malware class.

---

# 4. Feature Composition

The 318 selected features originate from four complementary feature sources.

| Feature Group | Number of Features | Primary Information |
|---|---:|---|
| API Functions | 200 | Windows API usage and capability-related signals |
| DLL Imports | 27 | Imported libraries and subsystem dependencies |
| PE Header | 46 | PE metadata and executable structural properties |
| PE Sections | 45 | Internal PE section organization and layout |
| **Total** | **318** | Unified static malware representation |

The four groups provide different perspectives on the same executable.

---

## 4.1 API Function Features

The API feature group contains 200 selected Windows API-related features.

These features provide static indicators of the Windows functionality represented in the executable.

Examples include API functions associated with:

- File operations
- Process operations
- Memory operations
- System information
- Thread management
- DLL loading
- Exception handling
- Registry/system operations
- Networking-related functionality

API features are primarily used as capability and behavioral indicators.

The presence of an API feature does not by itself prove that the corresponding behavior occurs during execution. The project uses these features as static evidence.

---

## 4.2 DLL Import Features

The DLL feature group contains 27 selected DLL-related features.

DLL imports provide information about the libraries and Windows subsystems that the executable depends upon.

DLL information complements API information:

- DLL features provide a broader library/subsystem view.
- API features provide a more specific function-level view.

Together they provide useful information about the functional profile of an executable.

---

## 4.3 PE Header Features

The PE Header feature group contains 46 selected features.

Examples include:

- `AddressOfEntryPoint`
- `TimeDateStamp`
- `SizeOfInitializedData`
- `SizeOfCode`
- `SizeOfImage`
- `CheckSum`
- `MajorLinkerVersion`
- `e_lfanew`
- `Characteristics`
- `DllCharacteristics`
- `Machine`
- `NumberOfSections`

These features describe structural and metadata characteristics of the Windows Portable Executable format.

They provide information about how the executable is constructed rather than directly representing runtime behavior.

---

## 4.4 PE Section Features

The PE Section feature group contains 45 selected features.

These describe properties of PE sections such as:

- `.text`
- `.data`
- `.rsrc`
- Other available sections

Examples of section characteristics include:

- Virtual size
- Raw data size
- Virtual address
- Pointer to raw data

These features provide information about the internal organization and layout of the executable.

---

# 5. Unified Malware Representation

The four feature groups are combined to form a unified 318-dimensional static representation.

Conceptually:

```text
Windows PE Sample
       |
       +----------------------+
       |                      |
       v                      v
 API Functions           DLL Imports
       |                      |
       +----------+-----------+
                  |
                  v
           PE Structure
            /       \
           v         v
      PE Header   PE Sections
           \         /
            \       /
             v     v
        318 Features
             |
             v
       Malware Analysis