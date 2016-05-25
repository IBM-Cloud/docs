---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 管理仪表板和模板
{: #managing-dashboards}

来自 IoT 设备的实时数据会显示在可定制仪表板中。可以手动创建仪表板来显示实时度量值、显示图形，以及显示一个或多个设备的其他信息。此外，仪表板还可以包含过滤的设备列表以及其他仪表板的链接。
{: shortdesc}

除了手动创建的仪表板外，{{site.data.keyword.iotrtinsights_short}} 还在**仪表板 > 概述**中随附有预定义的设备警报仪表板，并可根据创建的消息模式动态创建设备仪表板。

## 仪表板
{: #dashboards}

管理员可以创建新仪表板，也可以修改现有仪表板来显示关注的设备数据。  
要创建仪表板，请执行以下步骤：
1.	转至**仪表板 > 浏览仪表板**。
2.	单击**添加新仪表板**。
3.	为仪表板命名，然后选择属性，例如图标和背景。另外选择是否要使此仪表板可供 {{site.data.keyword.iotrtinsights_short}} 操作员用户编辑。
4.	单击 ![“创建”图标。](images/create.png "“创建”图标")。
5.	单击“新建仪表板”磁贴以打开空仪表板。
6.	要向仪表板添加窗口小部件，请执行以下步骤：  
 1.	单击**添加新组件**以添加初始仪表板窗口小部件。
 2.	选择要添加的组件，然后选择其他组件属性，并根据需要选择显示属性。例如，要显示设备的特定数据点的数字值，请选择`设备`，然后选择要添加的设备。在仪表板编辑器中的“可视化”下，选择要显示的数据点。然后，将新添加的窗口小部件放置到仪表板网格中。
 3.	单击 ![“创建”图标。](images/create.png "“创建”图标") 以向仪表板添加窗口小部件。
7.	仪表板会使用新添加的窗口小部件进行更新，并显示所选数据点定义的实时数据。

>**提示：**要创建列出所有设备的仪表板，请执行以下步骤：  
1. 转至**仪表板 > 浏览仪表板**，然后单击**添加新仪表板**。
2. 为仪表板提供描述性名称，例如`所有设备`，然后单击 ![“创建”图标。](images/create.png "“创建”图标")。
3. 在“仪表板”面板中，单击该仪表板，然后添加**添加新组件**。
4. 选择**容器**组件，然后选择**过滤的设备**以创建所有设备的列表。
5. 单击 ![“创建”图标。](images/create.png "“创建”图标")。  

>您的设备已列在新仪表板中。单击“设备”图标可打开设备仪表板，并查看该设备的实时数据。
### 仪表板窗口小部件
{: #dashboard-widgets}

仪表板由窗口小部件构成，窗口小部件用于显示来自一个或多个设备的实时数据。窗口小部件的行为取决于其类型、显示的数据点以及模式中配置数据点的方式。  
例如，如果为“原始”数据点添加“设备”窗口小部件，那么该窗口小部件只会将原始数据显示为字符串。

但是，如果该数据点配置有最小值和最大值，那么可以选择将窗口小部件显示为量表。

还可以为数据点分配“传感器”类型，以启用特殊类型的可视化窗口小部件，从而更好地演示所显示传感器数据的类型。例如，可以选择传感器类型`点亮/熄灭`，以启用`普通指示灯（开/关）`可视化窗口小部件。

您还可以选择包含多个窗口小部件以用于同一仪表板中的同一数据点，以便并排显示原始数字值和湿度。![用于同一数据点的多个窗口小部件。](images/widgets.svg "“用于同一数据点的多个窗口小部件”图标")  
*用于同一数据点的三个可视化选项。*


窗口小部件 | 类型和可视化
------------- | -------------
设备 | 数据 - 设备数据点的实时值。如果数据点配置为包含最小值和最大值，那么可视化选项会包含将数据点显示为量表的选项。此外，如果数据点配置有传感器类型，那么还会提供其他可视化选项。
图表 | 图形 - 绘制一个或多个设备的数据点的实时值。
仪表板 | 仪表板或模板的链接。
文本 | 文本框 - 已设置格式的文本。
容器 | 容器窗口小部件的类型：<ul><li>所有仪表板 - 所有仪表板的链接列表。</li><li>过滤的设备 - 所有设备的列表，或者按名称或位置过滤的设备列表。</li><li>过滤的带警报设备 - 所有带警报的设备的列表，或者按名称或位置过滤的带警报设备列表。</li><li>设备警报 - 在“过滤的带警报设备”容器中选择的设备的警报列表。</li></ul>
特殊 | 特殊窗口小部件的类型：<ul><li>地图 - 用于查找所选设备的地图。</li><li>其他设备信息 - 有关所选设备的更多信息。</li></ul>

下表汇总了在消息模式中使用传感器类型属性配置了所选数据点时，设备窗口小部件可用的可视化选项。

数据点传感器类型 | 可视化选项 | 详细信息 | 支持的数据类型
------------- | ------------- | -------------
未选择 | 简单值 | - | String/Integer/Float
点亮/熄灭 | 普通指示灯（开/关） | 0=关 | Integer
打开/关闭 | 普通开关指示器（开/关） | 0=关 | Integer
温度传感器 | 通用温度计 | 不适用 | Integer/Float
温度控件 | 通用温度计 | 不适用 | Integer/Float
压力传感器 | 普通压力计 | 不适用 | Integer/Float
电池电量 | 普通电池窗口小部件（低/高） | 0=正常 | Integer
亮度 | 亮度指示器（暗/亮） | 0=暗 | Integer
窗口打开/关闭 | 普通窗口状态（已打开/已关闭） | 0=已关闭 | Integer
门打开/关闭 | 普通门状态（已打开/已关闭） | 0=已关闭 | Integer
湿度传感器 | 湿度状态（干燥/湿润） | 0=干燥 | Integer
耗电量 | 普通电表 | 不适用 | Integer/Float
能量计 | 简单值 | 不适用 | Integer/Float
百分比 | 简单百分比 (0-100) | 不适用 | Integer/Float
电压 | 普通电压表 | 不适用 | Integer/Float
电流 | 普通电流表 | 不适用 | Integer/Float
经度 | “特殊”>“地图”窗口小部件上的设备位置（还需要“纬度”窗口小部件） | **重要信息：**用于经度值的数据点必须在消息模式中分配有传感器类型“经度”。 | Float
纬度 | “特殊”>“地图”窗口小部件上的设备位置（还需要“经度”窗口小部件） | **重要信息：**用于纬度值的数据点必须在消息模式中分配有传感器类型“纬度”。 | Float  


## 缺省仪表板布局
{{site.data.keyword.iotrtinsights_short}} 随附预定义仪表板：“警报”仪表板和“设备”仪表板。

以下各表描述了预定义仪表板的窗口小部件和布局。
### “警报”仪表板（“仪表板”>“概述”）
此仪表板随产品一起提供，用于列出具有已开启警报的设备列表。可以选择设备来查看有关警报的详细信息，也可以单击“设备”图标打开“设备”仪表板来显示该设备的实时数据。

<table>
<thead>
<tr>
<th colspan="3">“警报”仪表板</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">容器：具有警报的设备</td>
<td style="width:30%">容器：设备的警报</td>
<td style="width:30%">特殊：其他设备信息</td>
</tr>
<tr>
<td style="width:30%"></td>
<td style="width:30%"></td>
<td style="width:30%">特殊：地图</td>
</tr>
</tbody>
</table>

*“警报”仪表板布局*

### “设备”仪表板
单击设备列表中的“设备”图标来打开设备的“设备”仪表板。数据点添加到消息模式后，还会添加到设备模板中作为窗口小部件，这将动态创建“设备”仪表板。管理员可以手动添加或除去窗口小部件。

<table>
<thead>
<tr>
<th colspan="3">“设备”仪表板</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">设备：数据点 1</td>
<td style="width:30%">设备：数据点 2</td>
<td style="width:30%">设备：数据点 3</td>
</tr>
<tr>
<td style="width:30%">设备：数据点 N</td>
<td style="width:30%"></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*预定义的设备仪表板布局*

### 仪表板示例：所有设备的列表
以下仪表板包含所有设备的列表，并在从列表中选择设备时提供该设备的信息。

<table>
<thead>
<tr>
<th colspan="3">“所有设备的列表”仪表板</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">容器：过滤的设备（未设置过滤参数）</td>
<td style="width:30%">特殊：其他设备信息</td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*“所有设备的列表”仪表板布局*

## 模板
{: #templates}

模板可控制特定设备类型的预定义仪表板的布局。管理员可以根据您的需要来修改这些预定义模板。例如，预定义模板仅包含常规数据点。可以根据需要添加图形和其他组件。

例如，用户可以访问预定义设备仪表板来查看基本设备数据，然后访问手动创建的模板的链接，该模板可能包含一组完整的实时图形。创建模板与创建仪表板非常类似。  

要修改预定义模板，请执行以下步骤：
1.	转至**仪表板 > 管理模板**。
2.	在“管理模板”面板中，找到“模板”磁贴，然后单击 ![“配置”图标。](images/gear.png "“配置”图标")** > 更改布局**以打开模板进行编辑。  
3.	向模板添加窗口小部件。
 1.	单击**添加新的模板组件**以添加初始模板窗口小部件。
 2.	选择要添加的组件，然后选择其他组件属性，并根据需要选择显示属性。  
 3.	单击 ![“创建”图标。](images/create.png "“创建”图标") 以向模板添加窗口小部件。
4.	编辑现有窗口小部件。
 1.	将鼠标悬停在模板窗口小部件上方，然后单击 ![“配置”图标。](images/gear.png "“配置”图标")。
 2.	修改组件及其属性，然后根据需要对窗口小部件重新定位。
 3.	单击 ![“创建”图标。](images/create.png "“创建”图标") 以更新窗口小部件。  

模板将使用您的更改进行更新。

<!-- Administrators can also manually add templates for specific device types. These templates can then be linked to from the predefined templates.  -->

<!-- To create a template:
1.	Go to **Dashboards > Manage templates**.
2.	Click **Add new template**.
3.	Give the template a name, select a device type and attributes such as icon and background.
4.	Click ![Create icon.](images/create.png "Create icon").
5.	The empty template opens.
6.	Add widgets to the template.  
For a list of widgets, see below.
 1.	Click **Add new component** to add an initial template widget.
 2.	Select a component to add, then select further component attributes and, if needed, select display properties.
 For example, ... Then position the newly added widget in the dashboard grid.
 3.	Click ![Create icon.](images/create.png "Create icon") to add the widget to the template.
7.	The template updates with the newly added widgets.

### Template widgets
Widget | Type and visualization
------------- | -------------
Device | Data - Real-time value of data points for the device. For a description of the available widget options, see [Dashboard widgets](#dashboard-widgets "Dashboard widgets") above.
Chart | Graph - Plot real-time values of data points for one or more devices.
Dashboard | Link to a dashboard or a template.
Text | Text box - Formatted text
Container | Types of containers:<ul><li>All dashboards – A linked list of all dashboards</li><li>Filtered devices – A list of all devices, or filtered by name or location</li><li>Filtered devices with alerts – A list of all devices with alerts, or filtered by name or location</li><li>Alerts for device – A list of alerts for a device that is selected in a Filtered devices with alerts container</li></ul>
Special | Types of special:<ul><li>Map – A map that locates the selected device</li><li>Additional device information – More information about the selected device</li></ul>

### Template example: Selected set of graphs
One way of using device templates is to expand on the predefined device template by creating specialized templates for a device type, and then linking these from the predefined template by using a Dashboard widget.

<table>
<thead>
<tr>
<th colspan="3">Descriptive graphs template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: ID</td>
<td style="width:30%">Graph: One data point</td>
<td style="width:30%">Graph: Another data point</td>
</tr>
<tr>
<td style="width:30%">Special: Additional device information</td>
<td style="width:30%">Text: Short description of how to <br>interpret the device data in the graphs.</td>
<td></td>
</tr>
</tbody>
</table>

*Descriptive graphs template*

Link to this template from a predefined device template:

<table>
<thead>
<tr>
<th colspan="3">Predefined device dashboard layout with link to template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: Datapoint 1</td>
<td style="width:30%">Device: Datapoint 2</td>
<td style="width:30%">Device: Datapoint 3</td>
</tr>
<tr>
<td style="width:30%">Device: Datapoint N</td>
<td style="width:30%"><b>Dashboard: Descriptive graphs template</b></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Predefined device dashboard layout with link to template* -->


## 重置预定义仪表板和模板
{: #resetting-dashboards}

如果修改了预定义模板，那么该模板不会再通过消息模式更新进行动态更新，您需要重置该仪表板或模板才能恢复原始布局和窗口小部件。
要重置预定义仪表板和模板，请执行以下步骤：
1.	转至**仪表板 > 管理模板**或**仪表板 > 浏览仪表板**。
2.	找到预定义模板或仪表板磁贴，然后单击 **![“配置”图标。](images/gear.png "“配置”图标") > 重置布局**以删除并重新创建模板。  

模板或仪表板已使用缺省窗口小部件集重新创建。
