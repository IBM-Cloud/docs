---



copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Accessibility features for {{site.data.keyword.Bluemix}}

Accessibility features assist users who have a disability, such as restricted mobility or limited vision, to use information technology content successfully.
{:shortdesc}

## Accessibility features

<!-- Describe any accessibility features that your product offers (even if the product does not meet ALL of the requirements). You can  document positive workarounds. One example of a positive workaround is during an installation, where the product's graphical user interface is not compliant, the user can use the silent installation method to complete the installation by using a console command.

Do not itemize every checkpoint that the product meets because many of the checkpoint requirements are internal requirements.

Use the following introductory sentence and list for this section.  If your product does not support a feature in the list, remove that list item. Add features to the list that are supported by your product. -->

{{site.data.keyword.Bluemix_notm}} includes the following major accessibility features:

* Keyboard-only operation
* Operations that use a screen reader

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


## Interface information

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

Review the following information about the {{site.data.keyword.Bluemix_notm}} user interface:

* If you are using a screen reader with the {{site.data.keyword.Bluemix_notm}} web user interface or product documentation, use the latest version of Internet Explorer with the latest release of the screen reader.

<!-- If your product excludes flashing or blinking text, objects, or other elements that have a flash or blink frequency
greater than 2 Hz and lower than 55 Hz, include the following sentence. -->

* The {{site.data.keyword.Bluemix_notm}} user interfaces do not have content that flashes 2 - 55 times per second.

<!-- If your web applications rely on cascading style sheets, include the following paragraph. Because the IBM Knowledge Center  infrastructure requires CSS (even though the topics in your product documentation does not require CSS),  the documentation essentially requires CSS. -->

* The {{site.data.keyword.Bluemix_notm}} web user interfaces rely on cascading style sheets to render content properly and to provide a usable experience. The application provides an equivalent way for low-vision users to use a user’s system display settings, including high-contrast mode. You can control font size by using the device or web browser settings.

<!-- If your web applications do NOT rely on cascading style sheets, include the following paragraph.  Because the IBM Knowledge Center infrastructure requires CSS (even though your product documentation does not require CSS), if the documentation is displayed by using IBM Knowledge Center, the documentation essentially requires CSS. "The {{site.data.keyword.Bluemix_notm}} web user interface does not rely on cascading style sheets to render content properly and to provide a usable experience. However, the product documentation does rely on cascading style sheets. IBM Knowledge Center provides an equivalent way for low-vision users to use a user’s system display settings, including high-contrast mode. You can control font size by using the device or browser settings."-->

<!-- Add the following statement if your product has a user interface that is viewed on a web browser. -->

* The {{site.data.keyword.Bluemix_notm}} web user interface includes WAI-ARIA navigational landmarks that you can use to quickly navigate to functional areas in the application.

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

## Related accessibility information

The {{site.data.keyword.Bluemix_notm}} web user interface accessibility compliance status is specifically for the {{site.data.keyword.Bluemix_notm}} product platform. There are sub-sections of the user interface that are owned by third party products or services that host content within the platform, for which the {{site.data.keyword.Bluemix_notm}} compliance record does not maintain or own the accessibility compliance status. This means that if you are accessing any user interface or documentation for a service, you must request the compliance statements for that service. For example, if you are using the OpenWhisk dashboard, an interface for IBM Containers, the Administration console for a local or dedicated environment, or an IoT service, you must request [product accessibility information ![External link icon](../icons/launch-glyph.svg)](http://www-03.ibm.com/able/product_accessibility/index.html){: new_window} for that interface or documentation.

The {{site.data.keyword.Bluemix_notm}} documentation accessibility compliance is specifically for the {{site.data.keyword.Bluemix_notm}} core platform information, and it does not extend to any services. From the homepage, the content is separated into two sections: "How to use the {{site.data.keyword.Bluemix_notm}} platform" and "How to use {{site.data.keyword.Bluemix_notm}} services." The available documentation for the {{site.data.keyword.Bluemix_notm}} platform is managed and reported in the {{site.data.keyword.Bluemix_notm}} product accessibility information that is available upon request. For compliance status for any service, you must request [product accessibility information ![External link icon](../icons/launch-glyph.svg)](http://www-03.ibm.com/able/product_accessibility/index.html){: new_window}.

In addition to standard IBM help desk and support websites, IBM has established a TTY telephone service for use by deaf or hard of hearing customers to access sales and support services:

TTY service
800-IBM-3383 (800-426-3383)
(within North America)

## IBM and accessibility

For more information about the commitment that IBM has to accessibility, see [IBM Accessibility ![External link icon](../icons/launch-glyph.svg)](www.ibm.com/able){: new_window}


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
