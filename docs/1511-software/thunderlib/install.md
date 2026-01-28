---
title: ThunderLib - Install
---

# Adding ThunderLib to Your Robot Project

1.  In WPILib VSCode, open the Command Palette (Ctrl+Shift+P) and select __WPILib: Manage Vendor Dependencies__
    <figure markdown="span">
    ![](../../assets/thunderlib/vscode_wpilib_manage_vendor_libraries.png){width="600"}
    </figure>
2. Select __Install new libraries (online)__.
    <figure markdown="span">
    ![](../../assets/thunderlib/vscode_wpilib_install_new_libraries_online.png){width="600"}
    </figure>
3. In the box, paste the ThunderLib vendor URL and press Enter:
```
https://frc1511.github.io/thunderlib/ThunderLib2026.json
```
<figure markdown="span">
![](../../assets/thunderlib/vscode_wpilib_thunderlib_install.png){width="600"}
</figure>

Now you should see a file named `ThunderLib2026.json` in the `vendordeps` folder of your robot project, and ThunderLib will be available to use in your robot code. You may need to rebuild your project for VSCode intellisense to recognize the new library.
