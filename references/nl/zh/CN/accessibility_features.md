---



copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix}} 的辅助功能

辅助功能旨在帮助身体有残疾的用户（如行动不便或视力受限）成功使用信息技术内容。
{:shortdesc}

## 辅助功能选项功能

<!-- Describe any accessibility features that your product offers (even if the product does not meet ALL of the requirements). You can  document positive workarounds. One example of a positive workaround is during an installation, where the product's graphical user interface is not compliant, the user can use the silent installation method to complete the installation by using a console command.

Do not itemize every checkpoint that the product meets because many of the checkpoint requirements are internal requirements.

Use the following introductory sentence and list for this section.  If your product does not support a feature in the list, remove that list item. Add features to the list that are supported by your product. -->

{{site.data.keyword.Bluemix_notm}} 包含以下主要辅助功能选项功能：

* 只需键盘的操作
* 使用屏幕朗读器的操作

<!-- The following official statement can only be used IF we are fully compliant

{{site.data.keyword.Bluemix_notm}} uses the latest W3C Standard, [WAI-ARIA 1.0 ![External link icon](../icons/launch-glyph.svg)](http://www.w3.org/TR/wai-aria/){: new_window} to ensure compliance to [US Section 508 ![External link icon](../icons/launch-glyph.svg)](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-section-508-standards/section-508-standards){: new_window} and [Web Content Accessibility Guidelines (WCAG) 2.0 ![External link icon](../icons/launch-glyph.svg)](http://www.w3.org/TR/WCAG20/){: new_window}. To take advantage of accessibility features, use the latest release of your screen reader in combination with the latest Internet Explorer web browser that is supported by this product.

The {{site.data.keyword.Bluemix_notm}} online product documentation and the {{site.data.keyword.Bluemix_notm}} user interface framework is enabled for accessibility.

-->

<!-- ## Keyboard navigation

Document unique keyboard accessibility features.  This includes keyboard shortcut keys that are unique to your
application. Document all keyboard navigation that does not follow documented system conventions.

If the software uses standard system keyboard shortcuts for navigation, they do not have to be documented.  For a list of  standard keyboard shortcuts for your operating system, see the keyboard assistance information for that system. For example, the  following common system keyboard shortcuts do not have to be documented:

- To traverse to the next interactive control in the tab index, press the Tab key.
- To expand or collapse a tree node, press the Right Arrow key or the Left Arrow key.
- To traverse a tree node, press the Up Arrow key or the Down Arrow key.
- To scroll all the way up or down a page, press the Home key or the End key.
- To print the current page or active frame, press the Ctrl+P keys.

When the documentation provides instructions for completing tasks using the mouse, include the instructions for doing those tasks using the keyboard if the keyboard instructions are unique.

Table 1. Keyboard shortcuts in {{site.data.keyword.Bluemix_notm}}

Modify the following table for your product; if your product uses no unique keyboard shortcuts, remove the table and introductory sentence.

| **Action** | **Shortcut for Internet Explorer** |  **Shortcut for Firefox** |
| | | |
|Example: Move to the Contents View frame  | Alt+C, then press Enter and Shift+F6 | Shift+Alt+C and Shift+F6   |

-->


## 界面信息

<!-- Include details about user preferences, any unique or difficult-to-accomplish tasks, any known workarounds, or information about using assistive technologies that might be useful to a user with disabilities.

If you can, tell users how to perform basic accessibility tasks such as the ones in the following list:
- Adjust the volume
- Replace sounds with text
- Change fonts (if not done through the operating system)
- Disable animation
- Customize the response times for timed actions
- Use a screen reader with your product
- Use speech recognition software with your product
- Enable high contrast or large fonts (if not done through the operating system)
 -->

复查 {{site.data.keyword.Bluemix_notm}} 用户界面的以下信息：

* 如果您对 {{site.data.keyword.Bluemix_notm}} Web 用户界面或产品文档使用屏幕朗读器，请使用最新版本的 Internet Explorer 和最新版本的屏幕朗读器。

<!-- If your product excludes flashing or blinking text, objects, or other elements that have a flash or blink frequency
greater than 2 Hz and lower than 55 Hz, include the following sentence. -->

* {{site.data.keyword.Bluemix_notm}} 用户界面没有每秒闪烁 2 - 55 次的内容。

<!-- If your web applications rely on cascading style sheets, include the following paragraph. Because the IBM Knowledge Center  infrastructure requires CSS (even though the topics in your product documentation does not require CSS),  the documentation essentially requires CSS. -->

* {{site.data.keyword.Bluemix_notm}} Web 用户界面依靠级联样式表来正确呈现内容并提供有用的经验。该应用程序为弱视用户提供了同等方式来使用用户的系统显示设置，包括高对比度模式。您可以通过使用设备或 Web 浏览器设置来控制字体大小。

<!-- If your web applications do NOT rely on cascading style sheets, include the following paragraph.  Because the IBM Knowledge Center infrastructure requires CSS (even though your product documentation does not require CSS), if the documentation is displayed by using IBM Knowledge Center, the documentation essentially requires CSS. "The {{site.data.keyword.Bluemix_notm}} web user interface does not rely on cascading style sheets to render content properly and to provide a usable experience. However, the product documentation does rely on cascading style sheets. IBM Knowledge Center provides an equivalent way for low-vision users to use a user’s system display settings, including high-contrast mode. You can control font size by using the device or browser settings."-->

<!-- Add the following statement if your product has a user interface that is viewed on a web browser. -->

* {{site.data.keyword.Bluemix_notm}} Web 用户界面包含一些 WAI-ARIA 导航地标，以用于快速浏览至该应用程序中的各个功能区域。

<!-- ## Mobile applications

Describe accessibility features that your product offers for mobile applications:
- Describe any keyboard shortcuts that are not documented in IOS.  Also, describe shortcut keys that are in imbedded user assistance.

- Describe the order of navigation (especially those that run on a larger format like an iPad). A larger format can make using a keyboard difficult to get to items in the focus area. For example, for a mailbox, you might need to document the recommended sequence of keystrokes to get to a place in the UI (like getting to the first item in the third column, in a 3-colum display).

- Describe extensively used hints. Some users do not always enable hints. When hints are well documented, it can be helpful to the user so they can understand the mobile application better.

- Describe any accessibility-related options, for example, font size, color, or contrast. For example, if your mobile application implements the ability to use large fonts, document that feature. You might also need to describe which portions of the application react to a change in the option and which do not. If your application supports the operating system settings for font, size, and contrast, you do not need to document that fact. However, document changes to system settings (for example, if your mobile application uses a unique skin).

- Describe unique gestures: Use the following statement if your product uses standard operating system gesture navigation. If your product does not use standard gestures, omit the following sentence.

This product uses standard gestures.

If your mobile application has custom gestures, describe the gesture and the how to make it accessible. Document gestures where actions are assigned to a screen element (icons). Describe gestures that allow the user to interface with a page.  For example, if a page has a widget, describe the gesture with which the user can interface with the page. Use the following introductory sentence and list:

{{site.data.keyword.Bluemix_notm}} uses the following unique gestures

- item 1
- item 2

 Describe spatial orientation features. Spatial orientation can be very useful in a touch screen (for example, list on the left, content on the right, menu bar on the top, and a user decides to explore the screen). Document a spatial orientation feature if it’s a significant  feature or departure from the standard. For a user interface, describe the layout of the interface for the individual who can’t see it to know how things are oriented. Use correct wording like “You set the navigation in the area on the right side.” -->

## 辅助功能选项相关信息

{{site.data.keyword.Bluemix_notm}} Web 用户界面辅助功能选项合规性状态专用于 {{site.data.keyword.Bluemix_notm}} 产品平台。在用户界面中存在由第三方产品或服务所有的子部分，这些产品和服务在平台中托管内容，而 {{site.data.keyword.Bluemix_notm}} 合规性记录不会为该平台维护或拥有辅助功能选项合规性状态。这表示如果您访问服务的任何用户界面或文档，您必须为该服务请求合规性声明。例如，如果您使用 OpenWhisk 仪表板、IBM Containers 的界面、本地或专用环境的管理控制台或 IoT 服务，那么您必须为该界面或文档请求[产品辅助功能选项信息 ![外部链接图标](../icons/launch-glyph.svg)](http://www-03.ibm.com/able/product_accessibility/index.html){: new_window}。

{{site.data.keyword.Bluemix_notm}} 文档辅助功能选项合规性专用于 {{site.data.keyword.Bluemix_notm}} 核心平台信息，不会扩展到任何服务。在主页中，内容分成两个部分：“如何使用 {{site.data.keyword.Bluemix_notm}} 平台”和“如何使用 {{site.data.keyword.Bluemix_notm}} 服务”。{{site.data.keyword.Bluemix_notm}} 平台的可用文档在请求时即提供的 {{site.data.keyword.Bluemix_notm}} 产品辅助功能选项信息中管理和报告。要获取任何服务的合规性状态，您必须请求[产品辅助功能选项信息 ![外部链接图标](../icons/launch-glyph.svg)](http://www-03.ibm.com/able/product_accessibility/index.html){: new_window}。

除了标准 IBM 帮助热线和支持 Web 站点之外，IBM 还设立了 TTY 电话服务，供耳聋客户或听力困难的客户访问销售和支持服务：

TTY 服务 800-IBM-3383 (800-426-3383)（在北美地区）

## IBM 与辅助功能选项

有关 IBM 对辅助功能选项的承诺的更多信息，请参阅 [IBM 辅助功能选项 ![外部链接图标](../icons/launch-glyph.svg)](www.ibm.com/able){: new_window}


<!-- Add related links (at the bottom of this topic) to product documentation or online help that describes interface information (hardware or software) that pertains to the product accessibility features or functions.  For example, interface information might include wording similar to the following samples (these are excerpts from announcement letters):
- If PDF files are included, the files have limited accessibility support. With PDF documentation, you can use optional font enlargement, high-contrast display settings, and can navigate by keyboard alone.
- This product does not have audio features in its interface.
- When an applet, plug-in, or other application is required, it provides a link to one that is directly accessible, or provides alternate content for those that are not directly accessible.
- You can use supported screen readers with the user interface.
- Product_name has the following accessibility characteristics: <list of characteristics follows>
- The product_name online product documentation is available in IBM Knowledge Center, which is viewable from a standard web browser.

# rellinks
## general
*

-->
