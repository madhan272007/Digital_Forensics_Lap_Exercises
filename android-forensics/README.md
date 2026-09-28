# 🕵️‍♂️ Experiment 07 – Android Forensics (Logical Extraction using ADB)

## 🎯 Objective
To perform logical data acquisition from an Android smartphone using ADB commands and extract data such as contacts, call logs, messages, and device information.  
This experiment demonstrates a modern alternative to the deprecated AFLogical OSE tool.

---

## ⚙️ Tools & Requirements
Android Debug Bridge (ADB)  
Windows 10 / 11 with Git Bash or Command Prompt  
USB Cable & Android Smartphone (Debug Mode Enabled)  
Forensic Workstation Folder: C:\Forensics\AFLogicalData  

---

## 🧩 Procedure

### Step 1 – Enable Developer Options and USB Debugging
On your Android phone:  
Settings → About Phone → Tap Build Number (7 times)  
Then Settings → Developer Options → Enable USB Debugging  

---

### Step 2 – Verify Device Connection
adb devices  

**Expected Output**  
List of devices attached  
A65JUT5224000871   device  

---

### Step 3 – Start ADB Server (if not already running)
adb kill-server  
adb start-server  
adb devices  

---

### Step 4 – Create Extraction Directory on PC
mkdir -p /c/Forensics/AFLogicalData  

---

### Step 5 – Perform Logical Extraction Using ADB
adb shell "content query --uri content://contacts/phones/ > /storage/emulated/0/contacts.txt"  
adb shell "content query --uri content://sms/ > /storage/emulated/0/sms.txt"  
adb shell "content query --uri content://call_log/calls/ > /storage/emulated/0/calllog.txt"  
adb shell "getprop > /storage/emulated/0/deviceinfo.txt"  

✅ These commands extract Contacts, SMS, Call Logs and Device Info and store them as `.txt` files in `/storage/emulated/0/`.

---

### Step 6 – Verify Files on Device
adb shell  
ls /storage/emulated/0 | grep txt  

**Expected Output**  
contacts.txt  
sms.txt  
calllog.txt  
deviceinfo.txt  

exit  

---

### Step 7 – Pull Extracted Evidence to Local Workstation
adb pull /storage/emulated/0/contacts.txt C:\Forensics\AFLogicalData\  
adb pull /storage/emulated/0/sms.txt C:\Forensics\AFLogicalData\  
adb pull /storage/emulated/0/calllog.txt C:\Forensics\AFLogicalData\  
adb pull /storage/emulated/0/deviceinfo.txt C:\Forensics\AFLogicalData\  

Resulting Files:  
C:\Forensics\AFLogicalData\  
  ├── contacts.txt  
  ├── sms.txt  
  ├── calllog.txt  
  └── deviceinfo.txt  

---

### Step 8 – Verify Extracted Data
cd /c/Forensics/AFLogicalData  
ls  

cat contacts.txt | head  
cat sms.txt | head  
cat calllog.txt | head  
cat deviceinfo.txt | head  

---

### Step 9 – Move or Copy Screenshots for Documentation
mkdir -p /c/Users/krthc/Downloads/digital-forensics-experiments-2025/exp07-android-forensics/screenshots  
cp "/c/Users/krthc/OneDrive - Personal/Pictures/Screenshots/"*.png /c/Users/krthc/Downloads/digital-forensics-experiments-2025/exp07-android-forensics/screenshots/  

---

## 🔍 Observation
ADB commands allow controlled access to logical data without requiring root privileges.  
This method retrieves call logs, messages, contacts, and system details securely.  
It acts as a modern CLI-based replacement for the AFLogical OSE forensic application.  

---

## ✅ Result
Logical extraction was successfully performed using ADB.  
Extracted artifacts (Contacts, SMS, Call Logs, and Device Info) were pulled and verified.  
All evidence files were stored in the forensic workstation for further analysis.  

---
