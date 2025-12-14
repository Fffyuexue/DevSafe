中文 ： https://github.com/Fffyuexue/DevSafe/blob/main/README-Chinese.md
# DevSafe Module Documentation (English)

## I. Module Overview

**DevSafe** is a **KernelPatchModule (hereinafter referred to as KPM)** developed by  
**Kasuga Yuzuki**, designed to protect **Android device image partitions**.

The module aims to prevent malicious or abnormal modifications to runtime image partitions,  
thereby avoiding **irreversible system damage or potential financial loss**.  
It is positioned as a **security-first, functionality-oriented** low-level protection module.

DevSafe can operate within Root implementations that support KPM execution, including:

- FolkPatch  
- APatch  

Users may choose to **embed** or **dynamically load** the module according to their preferences.

---

## II. Terminology and Scope Statement

Within this document, the term **“image partition”** specifically refers to  
the Android system block device nodes under **`/dev/block`**, including the underlying physical block device partitions they map to.

All descriptions related to writing, interception, protection, or modification of image partitions  
**are strictly limited to `/dev/block` and its associated image partition scope**,  
and do not include user data partitions or non–block-device paths.

Before performing any operation involving `/dev/block`, users are strongly advised to  
fully understand the associated risks and ensure that DevSafe runtime parameters are correctly configured.

---

## III. Operational Principles

Under **normal circumstances**, once DevSafe is enabled:

- The module automatically intercepts abnormal write attempts to image partitions  
- No additional user interaction is required  

However, in scenarios where **legitimate image partition writes are required**,  
the module behavior must be adjusted by **passing runtime parameters**.

---

## IV. Scenarios Requiring Parameter Adjustment

Please ensure proper parameter configuration before performing the following operations:

1. System OTA updates  
2. Installation or removal of other KPM modules  
3. Maintenance or modification operations involving image partitions  
4. Any other actions that require writing to image partitions  

---

## V. Parameter Description (Effective Immediately)

DevSafe allows real-time control of its protection status via parameters.  
All parameter changes take effect **immediately**.

### Parameter `"0"` — Disable Protection

- Disables interception of image partition write operations  
- Allows all legitimate writes to proceed normally  

Applicable scenarios include:

- Prior to system OTA updates  
- When installing or uninstalling other KPM modules  
- When the Root implementation needs to write data into image partitions  

In this state, DevSafe will not interfere with any image partition write operations.

---

### Parameter `"1"` — Enable Protection

- Enables image partition write protection  
- Restores interception of abnormal or unauthorized write attempts  

After completing any operation that requires image partition writes,  
users are strongly advised to **immediately re-pass parameter `"1"`**  
to return the device to a protected state.

---

## VI. Update and Maintenance Notes

Due to the **time-sensitive nature** of DevSafe’s functionality,  
and the fact that **KernelPatch currently does not provide a cloud update mechanism**, users should:

- Regularly visit the project’s GitHub repository  
- Check for module updates or compatibility adjustments in a timely manner  
- Verify module status after major system or KernelPatch changes  

---

## VII. Summary

DevSafe is a professional protection module designed for low-level system security scenarios.  
Its correct usage relies on a clear understanding of system operation workflows.

**Disabling protection before image partition writes and restoring it immediately afterward  
is essential for maintaining device security and long-term system stability.**
