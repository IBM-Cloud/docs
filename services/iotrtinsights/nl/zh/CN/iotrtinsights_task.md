---

copyright:
  years: 2015,2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 连接和查看设备
{: #iotrtinsights_task}
*上次更新时间：2016 年 2 月 11 日*

{{site.data.keyword.iotrtinsights_short}} 使用 {{site.data.keyword.iot_short}} 来访问设备和检索数据。连接到 {{site.data.keyword.iot_short}} 的设备会自动连接到 {{site.data.keyword.iotrtinsights_short}}。
{: shortdesc}

如果要连接到新类型的设备，那么还必须配置消息模式，以映射设备数据点、设置单位以及对设备类型命名。如果设备属于已经配置的设备类型，那么其数据会自动显示在仪表板中。

## 添加新设备
{: #iotrtinsights_subtask}

要添加新设备，请执行以下步骤：  
添加新设备是分两步执行的过程。第一步是将设备添加到 {{site.data.keyword.iot_short}}，第二步是配置 {{site.data.keyword.iotrtinsights_short}} 使用并显示设备数据的方式。
1. 将设备添加到 {{site.data.keyword.iot_short}}。
> **提示：**如果部署了 Internet of Things 手机应用程序，那么 iotphone 设备已经添加到 *iot-phone-iotf-service* {{site.data.keyword.iot_short}}，因此可以跳过此步骤。  

  要将新设备添加到 {{site.data.keyword.iot_short}}，请参阅 [{{site.data.keyword.iot_full}} 文档](https://www.ng.bluemix.net/docs/services/IoT/index.html)和 [{{site.data.keyword.iot_short}} device connection recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF)。
2. 在 {{site.data.keyword.iotrtinsights_short}} 中配置设备。  
  1. 以管理员用户身份登录到 {{site.data.keyword.iotrtinsights_short}} 控制台。
  9. 转至**设备 > 浏览设备**，然后验证新添加的设备是否已列出。
  > **提示：**设备列表每分钟从数据源刷新一次。单击**刷新**可立即更新设备列表。
  3. 转至**设备 > 管理模式**，然后单击**添加新的消息模式**。  
  4. 为消息模式输入名称，例如：
  `新消息模式`。
  5. 单击**链接新数据源**，然后选择对应于 {{site.data.keyword.iot_short}} 实例和设备的数据源和设备类型。（可选）输入事件名称以只收集该事件的数据，或者保留 `+` 通配符以收集所有事件。有关如何确定设备的事件类型的更多信息位于[此处](#identify-datapoints "确定数据点。")。  
  >**重要信息：**每个消息模式都必须具有数据源、设备类型和事件名称的唯一组合。要为特定数据源和设备类型组合创建多个模式，请为每个消息模式指定唯一事件名称，而不要使用缺省的 `+` 通配符。   
  6. 添加要包含在“设备”仪表板中的一个或多个数据点。
    可以从已连接设备中选择数据点，也可以手动添加数据点。可用数据点在设备发送的消息的有效内容中进行定义。有关 {{site.data.keyword.iot_short}} 有效内容格式的信息，请参阅 {{site.data.keyword.iot_short}} 文档中的[消息有效内容](https://docs.internetofthings.ibmcloud.com/messaging/payload.html "消息有效内容。")主题。   
    > **提示：**您可以手动创建虚拟数据点，以用于修改或组合类型为整数或浮点数的现有数据点。例如，如果设备数据点 temp 返回华氏温度值，但您希望改为使用摄氏温度值，那么可以使用函数 *temp_c=(temp-32)/1.8* 来创建虚拟数据点 *temp_c*。然后，可以使用虚拟 *temp_c* 数据点，而不使用规则条件中的实时 *temp* 数据点。在仪表板中，虚拟数据点会用虚线下划线进行标识。    

  <dl>
  <dt>从已连接设备中进行选择</dt>
  <dd>
  <ol>
    <li>单击**从已连接设备中进行选择**。</li>  
    <li>在“添加数据点”对话框中，选择要添加的一个或多个数据点，然后单击**确定**。</li>   
    <li>所选数据点已添加，并包含设置为数据点名称的描述。单击列表中的数据点以对其进行编辑，然后添加其他属性，例如传感器类型、数据类型和小数位数。</li>
  </ol>
  </dd>
  <dt>手动添加</dt>
  <p><b>提示：</b>要创建[嵌套数据点结构](schemas.html)，请首先添加数据类型为“父代”的数据点。然后，在数据点表中，可以单击 ![“添加子代”图标。](images/add_child.png "添加子代") 以添加一个或多个子数据点。</p>
  <dd>
  <ol>
    <li>单击**手动添加**。</li>
    <li>选择**实时数据点**或**虚拟数据点**。</br></li>
    <li>定义以下数据点信息：
    <ul>  
     <li> 数据点 - 您在 [{{site.data.keyword.iot_short}} 仪表板中找到](#identify-datapoints "确定数据点。")的数据点标识。例如：  
   `id`、`ts` 或 `lat`  </li>
     <li>描述 - 数据点的简短描述。在仪表板中显示数据点时会使用此描述。</li>
     <li>虚拟数据点函数 - 添加一个或多个组件以定义有效函数。可以使用数据点、数字值和数学运算符（例如 +、-、\*、/、( 和 )）来构建函数。</li>
     <li>数据类型 - 数据点的数据的类型：  
   `字符串`、`整数`、`浮点数`或`父代`。</li>
     <li>传感器类型 -（可选）选择如何在仪表板中解释数据点。根据类型和传感器类型组合，可能会有其他可视化选项可供仪表板窗口小部件使用。有关传感器类型和可视化选项的更多信息，请参阅[仪表板窗口小部件](dashboards.html#dashboard-widget "仪表板窗口小部件")。</li>
     <li>数据点图标 -（可选）选择用于在仪表板窗口小部件中表示数据点的图标。</li>
     <li>最小值/最大值 -（可选）仅限整数和浮点数：如果输入了最大值和最小值，那么设备数据可以在仪表板中显示为量表。</li>
     <li>数据单位 -（可选）：数据点的数据的单位。例如：  
     `C` 或 `Mph`</li>
     <li> 小数位数 -（可选）仅限浮点数：要在设备数据中包含的小数位数。</li>
    </ul>
    </li>
  </ol>
  </dd>
  </dl>
   8. 单击**确定**以创建消息模式。
   9. 转至**设备 > 浏览设备**，然后单击新添加的设备，以验证实时设备数据是否已显示，以及数据点是否已正确映射。

## 在 {{site.data.keyword.iot_short}} 仪表板中确定数据点和事件。
{: #identify-datapoints}
   可以在 {{site.data.keyword.iot_short}} 仪表板中找到设备的数据点和事件类型。
   >**提示：**如果是使用 Internet of Things 手机应用程序作为 IoT 设备，那么可以使用 sensorData 事件和以下数据点来配置消息模式：
   >- d.id - 设备标识
   >- d.ts - 时间戳记
   >- d.lat - 纬度
   >- d.lng - 经度
   >- d.ax - X 轴加速
   >- d.ay - Y 轴加速
   >- d.az - Z 轴加速
   >- d.oa - α 运动
   >- d.ob - β 运动
   >- d.og - γ 运动
   >其中，d.*datapoint* 表示数据点嵌套在消息有效内容中类型为“父代”的 d 数据点下。

   1. 在 Bluemix 仪表板中，单击 Internet of Things 磁贴。  
   >**注：**如果使用的是 Internet of Things 手机应用程序，请单击 *iot-phone-iotf-service* 磁贴。  
   2. 单击**启动仪表板**以打开 {{site.data.keyword.iot_short}} 仪表板。
   3. 转至**设备**页面。
   4. 单击您的设备以打开“设备详细信息”页面。
     向下滚动到**传感器信息**部分，以查看设备的可用事件和数据点的列表。在 {{site.data.keyword.iotrtinsights_short}} 中配置设备时，这些信息是必需的。
