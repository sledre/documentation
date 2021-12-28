---
title: "Ghidra Extension"
date: 2021-09-12T12:41:48+02:00
draft: false
weight: 10
---

### Installation

Start by downloading the latest version of the [SledRE Ghidra extension](https://github.com/sledre/ghidra-sledre/releases) corresponding to your version.  

Then, open *Ghidra*, go to *File* and click on *Install Extensions...*.
![Extension install button](/images/ghidra/extension-install-button.png?classes=border,shadow&height=400px)

Click on the *green cross* at the upper right of the window and select the *Ghidra SledRE* release you previously downloaded, then press *Ok*.

![Extension selection form](/images/ghidra/extension-select-form.png?classes=border,shadow&height=300px)

You should now have a popup telling you to restart *Ghidra*.

![Ghidra restart](/images/ghidra/ghidra-restart.png?classes=border,shadow&height=130px)

After, the restart, you'll have another pop asking if you want to configure newly installed extension. Press *yes*.

![Configure new extensions](/images/ghidra/config-new-extensions.png?classes=border,shadow&height=130px)

Then, a new window will be opened. Make sure to enable the extension by clicking on the little box and press the button *Ok*.

![Enable the extension](/images/ghidra/enable-extension.png?classes=border,shadow&height=350px)

You should now see the SledRE extension UI.

![SledRE plugin UI](/images/ghidra/sledre-ui.png?classes=border,shadow&height=400px)

{{% notice note %}}
If it's not the case, in *Ghidra* click on the *Window* menu and then on *Sledre* to render the windows.
![Windows menu](/images/ghidra/window-menu.png?classes=border,shadow&height=400px)
{{% /notice %}}

### Usage

#### Configure SledRE
The **Ghidra Extension** needs to be linked to an active SledRE API.  
To do that, click on the *Configure SledRE URL* button. A popup window will appear where you can input **SledRE** URL.

![SledRE plugin configuration](/images/ghidra/sledre-url-input.png?classes=border,shadow&height=150px)

If the **Ghidra Extension**  is connected to **SledRE**, the status will be updated.

![SledRE plugin status](/images/ghidra/sledre-success-conn.png?classes=border,shadow&height=350px)

#### Run analysis

 now run a job on the sample that is opened in **Ghidra**.  
The sample must be in *Windows PE format*.  
You can click on the *Start SledRE analysis* button. A popup will appear during the analysis, but you can continue navigating on Ghidra.

![SledRE plugin analysis popup](/images/ghidra/sledre-analysis-popup.png?classes=border,shadow&height=150px)

When the analysis if finished, the **SledRE** status should go from *Running* to *Connected* again. If SledRE generated traces, they will be present inside the table.

![SledRE plugin resutls](/images/ghidra/sledre-results.png?classes=border,shadow&height=400px)

#### Using the results
You can go to the instruction that called the function referenced inside the table by double clicking on the table row.  
You can also click on the button *Add traces comments* to append comments directly in the listing and decompiler views.

![SledRE plugin comments](/images/ghidra/ghidra-comments.png?classes=border,shadow&height=150px)