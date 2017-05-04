---



copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix}}의 접근성 기능

접근성 기능을 사용하면 거동이 불편하거나 시각 장애가 있는 사용자도 정보 기술 컨텐츠를 정상적으로 사용할 수 있습니다.
{:shortdesc}

## 접근성 기능

<!-- Describe any accessibility features that your product offers (even if the product does not meet ALL of the requirements). You can  document positive workarounds. One example of a positive workaround is during an installation, where the product's graphical user interface is not compliant, the user can use the silent installation method to complete the installation by using a console command.

Do not itemize every checkpoint that the product meets because many of the checkpoint requirements are internal requirements.

Use the following introductory sentence and list for this section.  If your product does not support a feature in the list, remove that list item. Add features to the list that are supported by your product. -->

{{site.data.keyword.Bluemix_notm}}에는 다음과 같은 주요 접근성 기능이 포함되어 있습니다. 

* 키보드 전용 작업
* 스크린 리더를 사용하는 작업

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


## 인터페이스 정보

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

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에 대한 다음 정보를 검토하십시오.

* {{site.data.keyword.Bluemix_notm}} 웹 사용자 인터페이스나 제품 문서에 스크린 리더를 사용하는 경우, 스크린 리더의 최신 릴리스와 최신 버전의 Internet Explorer를 사용하십시오.

<!-- If your product excludes flashing or blinking text, objects, or other elements that have a flash or blink frequency
greater than 2 Hz and lower than 55 Hz, include the following sentence. -->

* {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에 초당 2 - 55회 깜빡이는 컨텐츠가 없습니다. 

<!-- If your web applications rely on cascading style sheets, include the following paragraph. Because the IBM Knowledge Center  infrastructure requires CSS (even though the topics in your product documentation does not require CSS),  the documentation essentially requires CSS. -->

* {{site.data.keyword.Bluemix_notm}} 웹 사용자 인터페이스는 캐스케이딩 스타일시트를 사용하여 컨텐츠를 올바르게 렌더링하고 사용 가능한 경험을 제공합니다. 애플리케이션은 시각 장애가 있는 사용자가 고대비 모드를 비롯한 사용자의 시스템 표시 설정을 사용할 수 있도록 동등한 방법을 제공합니다. 디바이스 또는 웹 브라우저 설정을 사용하여 글꼴 크기를 제어할 수 있습니다. 

<!-- If your web applications do NOT rely on cascading style sheets, include the following paragraph.  Because the IBM Knowledge Center infrastructure requires CSS (even though your product documentation does not require CSS), if the documentation is displayed by using IBM Knowledge Center, the documentation essentially requires CSS. "The {{site.data.keyword.Bluemix_notm}} web user interface does not rely on cascading style sheets to render content properly and to provide a usable experience. However, the product documentation does rely on cascading style sheets. IBM Knowledge Center provides an equivalent way for low-vision users to use a user’s system display settings, including high-contrast mode. You can control font size by using the device or browser settings."-->

<!-- Add the following statement if your product has a user interface that is viewed on a web browser. -->

* {{site.data.keyword.Bluemix_notm}} 웹 사용자 인터페이스에는 애플리케이션의 기능 영역을 빠르게 탐색하는 데 사용할 수 있는 WAI-ARIA 탐색 랜드마크가 포함되어 있습니다.

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

## 관련 접근성 정보

{{site.data.keyword.Bluemix_notm}} 웹 사용자 인터페이스 접근성 규제 준수 상태는 특별히 {{site.data.keyword.Bluemix_notm}} 제품 플랫폼을 위한 것입니다. 이 플랫폼에 컨텐츠를 호스팅하는 써드파티 제품 또는 서비스에서 소유한 사용자 인터페이스의 하위 섹션이 있기 때문에, {{site.data.keyword.Bluemix_notm}} 규제 준수 레코드에서 접근성 규제 준수 상태를 유지보수하거나 소유하지 않습니다. 이는 서비스의 사용자 인터페이스나 문서에 액세스하는 경우 해당 서비스에 대한 규제 준수 보고서를 요청해야 함을 의미합니다. 예를 들어, OpenWhisk 대시보드, IBM Containers용 인터페이스, 로컬 또는 전용 환경을 위한 관리 콘솔 또는 IoT 서비스를 사용하는 경우, 해당 인터페이스나 문서의 [제품 접근성 정보 ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://www-03.ibm.com/able/product_accessibility/index.html){: new_window}를 요청해야 합니다.

{{site.data.keyword.Bluemix_notm}} 문서 접근성 규제 준수는 특별히 {{site.data.keyword.Bluemix_notm}} 코어 플랫폼 정보에 적합하고, 이는 서비스로 확장되지 않습니다. 홈 페이지에서, 컨텐츠가 두 개의 섹션으로 나뉩니다. "{{site.data.keyword.Bluemix_notm}} 플랫폼 사용 방법" 및 "{{site.data.keyword.Bluemix_notm}} 서비스 사용 방법". {{site.data.keyword.Bluemix_notm}} 플랫폼의 사용 가능한 문서는 요청 시 사용할 수 있는 {{site.data.keyword.Bluemix_notm}} 제품 접근성 정보에서 관리되고 보고됩니다. 서비스의 규제 준수 상태에 대해 [제품 접근성 정보 ![외부 링크 아이콘](../icons/launch-glyph.svg)](http://www-03.ibm.com/able/product_accessibility/index.html){: new_window}를 요청해야 합니다.

표준 IBM 헬프 데스크 및 지원 웹 사이트 외에도, IBM은 청각 장애가 있는 고객이 판매 및 지원 서비스에 접속할 수 있도록 TTY 전화 서비스를 신설하였습니다. 

TTY 서비스
800-IBM-3383 (800-426-3383)
(북미 지역)

## IBM 및 접근성 

IBM의 접근성 약정에 대한 자세한 정보는 [IBM Accessibility ![외부 링크 아이콘](../icons/launch-glyph.svg)](www.ibm.com/able){: new_window}를 참조하십시오.


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
