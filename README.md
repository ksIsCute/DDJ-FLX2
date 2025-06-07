# How to install the DDJ-FLX2 MIDI mapping on **Linux**:


### **Installation Steps**
#### **1. Locate Mixxx's Controller Directory**
Open a terminal and run:
```bash
# Create the directory if it doesn't exist
mkdir -p ~/.mixxx/controllers
```
The mapping file should go in:
```
~/.mixxx/controllers/
```

#### **2. Configure Mixxx**
1. **Launch Mixxx**.
2. Go to **Preferences**/**Controllers**.
3. Click **Add** and select **"Pioneer DDJ-FLX2"** from the dropdown.
4. Click **"Load Mapping"** and select `DDJ-FLX2.midi.js`.
5. Enable the controller by checking the **"Enabled"** box.
6. Click **OK** to save.

---

### **Verification**
1. **Test the Jog Wheels**:
   - **Touch the platter**: Should activate scratching (vinyl mode).
   - **Release touch**: Should switch to track seeking.
2. **Check MIDI Input** (Optional):
   - In Mixxx **Preferences** → **Controllers**, enable **"MIDI Debug"**.
   - Monitor if the controller sends signals when touching/jogging.

---

### **Troubleshooting**
#### **Issue: Jog Wheels Don't Respond**
- **Fix 1**: Ensure the controller is **USB-connected** and recognized:
  ```bash
  lsusb | grep "Pioneer"
  ```
  (Should show the DDJ-FLX2.)
- **Fix 2**: Verify Mixxx has **ALSA/JACK access**:
  ```bash
  groups | grep audio
  ```
  If missing, add your user to the `audio` group:
  ```bash
  sudo usermod -aG audio $USER
  ```
  (Log out and back in.)

#### **Issue: Scratching Feels Laggy**
- **Adjust sensitivity** in the script:
  ```javascript
  this.jogSensitivity = 0.7; // Increase (0.1–1.0)
  ```
  Save the file and **reload the mapping** in Mixxx.

#### **Issue: Touch Sensors Inverted**
- Modify the `touch1`/`touch2` functions:
  ```javascript
  engine.setValue(group, "vinylcontrol_enable", value ? 0 : 1);
  ```

---

### **Uninstall**
To remove:
1. Delete the mapping file:
   ```bash
   rm ~/.mixxx/controllers/DDJ-FLX2.midi.js
   ```
2. In Mixxx **Preferences** → **Controllers**, remove the FLX2 entry.

---

This follows Mixxx’s Linux MIDI guidelines and ensures proper jog/scratch behavior. Let me know if you hit any snags!
