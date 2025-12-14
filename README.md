中文 ： https://github.com/Fffyuexue/DevSafe/blob/main/README-Chinese.md
# DevSafe Module Documentation

## I. Module Overview

**DevSafe** is a **KernelPatchModule (hereinafter referred to as KPM)** developed by  
**春日ユズキ (Kasuga Yuzuki)**, designed to protect **Android device image partitions**.

The module aims to prevent malicious or abnormal modifications to the runtime image partitions,  
thereby avoiding **irreversible system damage or potential financial loss**.  
It is positioned as a **security-oriented, functionality-focused** core protection module.

DevSafe can operate within Root implementations that support KPM execution, including but not limited to:

- FolkPatch  
- APatch  

Users may choose to **embed** or **dynamically load** the module according to their preferences.

---

## II. Operational Principles

Under **normal circumstances**, once DevSafe is enabled:

- The module automatically protects image partitions from unauthorized write operations  
- No additional user interaction is required  

However, in certain scenarios where **legitimate image partition writes are necessary**,  
the module behavior must be adjusted by **passing runtime parameters**.

---

## III. Scenarios Requiring Parameter Adjustment

Please ensure proper parameter configuration before performing the following operations:

1. **System OTA updates**
2. **Installation or removal of other KPM modules**
3. **Maintenance or modification operations involving image partitions**
4. **Any other actions that require writing to image partitions**

---

## IV. Parameter Description (Effective Immediately)

DevSafe allows real-time control of its protection status via parameters.  
All parameter changes take effect **immediately**.

### 1. Parameter `"0"` — Disable Protection

**Description:**

- Completely disables image partition write interception  
- Allows all legitimate write operations to proceed without restriction  

**Applicable scenarios include (but are not limited to):**

- Prior to system OTA updates  
- When installing or uninstalling other KPM modules  
- When the Root implementation needs to write data into image partitions  

> In this state, DevSafe will not interfere with any image partition write operations.

---

### 2. Parameter `"1"` — Enable Protection

**Description:**

- Enables image partition write protection  
- Restores interception of abnormal or unauthorized write attempts  

**Usage recommendation:**

- After completing any operation that requires image partition writes  
- Immediately re-pass parameter `"1"`  
- To ensure the device returns to a protected state  

This parameter is typically used in conjunction with `"0"`,  
forming a clear **disable → operate → re-enable protection** workflow.

---

## V. Update and Maintenance Notes

Due to the **high time-sensitivity** of DevSafe’s functionality,  
and the fact that **KernelPatch currently does not provide a cloud update mechanism**, users should:

- Regularly visit the project’s **GitHub repository**
- Check for module updates or compatibility adjustments in a timely manner
- Verify module status after major system or KernelPatch changes

---

## VI. Summary

DevSafe is a professional protection module designed for low-level system security scenarios.  
Its correct usage relies on a clear understanding of system operation workflows.

**Always adjust parameters before writing to image partitions, and restore protection immediately after.**  
This practice is essential for maintaining device security and long-term system stability.
