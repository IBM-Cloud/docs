---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# 创建设备类型模式
{: #iotrtinsights_task}

要使用诸如规则和操作之类的 {{site.data.keyword.iot_short}} 功能，必须创建模式以将设备属性映射到用户友好的属性名称，为这些属性设置数据单位，并指定要用于模式的消息类型。
{: shortdesc}

**重要信息：**要使用规则和操作，模式是必需的。有关信息，请参阅 [Cloud Analytics](cloud_analytics.html#rules)。

**重要信息：**分析功能是从 {{site.data.keyword.iotrtinsights_full}} 服务合并进来的。如果您的 {{site.data.keyword.iot_short_notm}} 组织用作现有 {{site.data.keyword.iotrtinsights_short}} 实例的数据源，那么在迁移现有 {{site.data.keyword.iotrtinsights_short}} 实例后，才会启用 Cloud Analytics 和 Edge Analytics。继续使用 {{site.data.keyword.iotrtinsights_short}} 仪表板来满足分析需要，直到迁移完成。有关更多信息，请参阅 IBM developerWorks 上的 [IBM Watson IoT Platform 博客 ![外部链接图标](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} 以及现有 {{site.data.keyword.iotrtinsights_short}} 实例仪表板。  

## 添加设备模式
{: #add_schema}

要添加模式，请执行以下操作：  
1. 转至**设备 > 管理模式**，并单击**添加模式**。  
2. 选择要与此消息模式关联的设备类型。**重要信息：**对于一种设备类型，仅可定义一个模式。

3. 添加一个或多个属性。
      
您可以从连接的设备选择属性，创建用于修改或组合现有属性的虚拟属性，或手动添加属性。  

    **提示：**设备所发送的消息的有效内容中定义了可用属性。有关 {{site.data.keyword.iot_short}} 有效内容格式的信息，请参阅[消息有效内容](reference/mqtt/index.html#message-payloadl "消息有效内容。")主题。   
  <dl>
  <dt>手动添加属性</dt>
  <p><b>提示：</b>要创建嵌套属性结构，请首先添加具有 Parent 数据类型的属性。然后，可在属性表中单击 ![“添加子代”图标](images/add_child.png "添加子代") 以添加一个或多个子属性。</p>
  <dd>
  <ol>
    <li>选择**手动**选项卡。</li>
    <li>定义以下属性详细信息：
    <ul>  
      <li>名称 - {{site.data.keyword.iot_short}} 仪表板、菜单和向导中使用的属性的描述性名称。</li>
      <li>数据类型 - 属性的数据类型：  
   `String`、`Integer`、`Float` 或 `Parent`。</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>属性 - 属性标识，例如：  
 `temp` 或 `speed`  </br> 有关如何从设备消息识别属性的信息，请参阅[识别设备的属性](#identify-datapoints "识别属性。")。</li>
  <li>数据单位 - 可选：属性的数据单位。例如：  
     `C` 或 `Mph`  </li>
     <li> 小数位 - 可选，仅浮点型：设备数据中要包含的小数位数。</li>
    </ul>
    </li>
    <li>单击**完成**以创建属性。</li>
  </ol>
  </dd>
  <dt>创建虚拟属性</dt>
  <dd> 例如，如果设备属性 temp 以华氏度为单位返回温度值，而您希望改用摄氏度，那么可创建具有以下函数的虚拟属性 *temp_c*：*temp_c=(temp-32)/1.8*。然后，可在规则条件中使用虚拟 *temp_c* 属性而不是实时 *temp* 属性。  
  要创建虚拟属性，请执行以下操作：
  <ol>
    <li>选择**虚拟属性**选项卡。</li>  
    <li>定义以下属性详细信息：
    <ul>
    <li>名称 - {{site.data.keyword.iot_short}} 仪表板、菜单和向导中使用的属性的描述性名称。</li>
    <li>数据类型 - 属性的数据类型：  
 `Float` 或 `Integer`。</li>
 <li>属性 - 虚拟属性的属性标识。例如：  
`temp_virt`</li>
    <li>计算 - 添加一个或多个组件以定义有效函数。可使用属性、数字值和数学运算符，例如 +、-、\*、/、( 和 )。  
    对于一组公式单击**高级**，以用于边缘设备上的数据点序列。有关高级公式的更多信息，请参阅[边缘虚拟属性的高级计算](im_vir_calculations.html)。  
    **重要信息：**不支持用于基于高级公式比较虚拟属性的规则条件。</li>
    <li>数据单位 - 可选：属性的数据单位。例如：`C` 或 `Mph`</li>
    <li> 小数位 - 可选，仅浮点型：设备数据中要包含的小数位数。</li>
   </ul>
   </li>
   <li>单击**完成**以创建属性。</li>
  </ol>
  </dd>
  <dt>从连接的设备选择属性</dt>
  <dd>
  <ol>
    <li>选择**来自连接的设备**选项卡。</li>  
    <li>选择一个或多个属性以添加到模式。以后可编辑这些属性来设置特性，如名称和数据单位。  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>单击**确定**以创建属性。</li>
  </ol>
  </dd>
    <dd>已添加所选属性，并且描述已设置为属性的名称。单击列表中的属性以进行编辑，并添加额外的特性（例如，传感器类型、数据类型和小数位数）。</dd>
  </dl>
8. 单击**完成**以创建消息模式。

## 识别设备的属性。
{: #identify-datapoints}
   可以在 {{site.data.keyword.iot_short}} 仪表板中找到设备的属性。

1. 在 {{site.data.keyword.iot_short}} 仪表板中，转至**设备**。
2. 单击设备以打开显示设备详细信息的页面。
3. 向下滚动到**传感器信息**部分，以查看连接的设备的可用属性列表。
