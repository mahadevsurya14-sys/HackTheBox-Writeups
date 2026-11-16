# HTB Diagnostic – Challenge Writeup

**Platform:** Hack The Box  
**Challenge:** Diagnostic  
**Category:** Malware Analysis  
**Difficulty:** Easy  
**Status:** Completed  
**Date:** 16 November 2026  
**XP Earned:** 260

## Objective

Analyze a suspicious Microsoft Word document, investigate its external relationships, decode the embedded PowerShell payload, and identify the hidden indicator.

## Tools Used

- Kali Linux
- curl
- unzip
- grep
- Python 3
- Base64 decoder

## Investigation Methodology

### 1. Download and identify the document

Downloaded the provided document and identified its file format.

```bash
curl -v http://TARGET/layoffs.doc -o layoffs.doc
file layoffs.doc
```

### 2. Inspect the document structure

Since the document was an OOXML archive, inspected its contents.

```bash
unzip -l layoffs.doc
```

Examined:
- `word/document.xml`
- `word/_rels/document.xml.rels`

### 3. Identify the external OLE relationship

Found an external OLE object referencing an HTML resource.

The relationship used the `htmlfile` ProgID and an external URL.

### 4. Analyze the HTML payload

Retrieved the HTML resource for static analysis.

```bash
curl -v http://TARGET/payload.html -o payload1.html
```

Identified JavaScript that invoked the `ms-msdt:` protocol handler.

This behavior is associated with **Follina (CVE-2022-30190)**.

### 5. Decode the PowerShell payload

Extracted the Base64-encoded content and decoded it using Python.

```python
import base64

with open("encoded.txt") as f:
    data = f.read().strip().strip("'")

decoded = base64.b64decode(data)

with open("decoded.txt", "wb") as f:
    f.write(decoded)

print(decoded.decode("utf-8", errors="replace"))
```

### 6. Analyze obfuscated commands

Analyzed the decoded PowerShell script and reconstructed its obfuscated strings.

Identified:
- An `Invoke-WebRequest` download operation.
- A remote executable download location.
- A Windows Tasks directory as the destination.
- A subsequent attempt to execute the downloaded file.

## Key Learnings

- Understanding the internal structure of DOCX files.
- Investigating suspicious OLE relationships.
- Recognizing Follina-related behavior.
- Decoding Base64-encoded PowerShell.
- Analyzing obfuscated commands without executing the payload.
- Practicing safe static malware analysis.

## Conclusion

Successfully completed the HTB Diagnostic challenge through document inspection, static analysis, Base64 decoding, and PowerShell deobfuscation.

**Key takeaway:** Never execute suspicious document payloads during initial analysis. Static analysis can reveal valuable indicators while reducing risk.

**Challenge Status:** Completed ✅
