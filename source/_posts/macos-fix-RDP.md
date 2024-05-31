---
title: Mac-RDP
date: 2016-09-01 09:09:22
tags: [tools, Mac]
---

**mac远程桌面连接windows 8.1 update，提示： 远程桌面连接无法验证您希望连接的计算机的身份**

**Solution:**

> Verify that the firewall **allows** remote desktop connections with **RDP** (Port 3389)


- Click **Start/Run**. Type `gpedit.msc` and click **OK** to open **The Group Policy Editor**.

-  In the left hand sidebar, **expand**
    1. Computer Configuration
    2. Administrative Templates
    3. Windows Components
    4. Remote Desktop Session Host

- Select **Security**. Change **Require use of specific security layer for remote desktop (RDP) connection** to **Enabled**

- and select **RDP** in the **Options** pane. Change **Require user authentication for remote connections by using Network Level Authentication** to **Disabled**

- Close **Group Policy Editor** and **reboot** the machine for changes to take effect.

<!-- more -->
