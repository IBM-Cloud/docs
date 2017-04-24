---



copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Funzioni di accesso facilitato per {{site.data.keyword.Bluemix}}

Le funzioni di accesso facilitato aiutano un utente con disabilità fisiche, quali una mobilità ridotta o una vista limitata, a utilizzare prodotti software.
{:shortdesc}

## Funzioni di accesso facilitato

<!-- Describe any accessibility features that your product offers (even if the product does not meet ALL of the requirements). You can  document positive workarounds. One example of a positive workaround is during an installation, where the product's graphical user interface is not compliant, the user can use the silent installation method to complete the installation by using a console command.

Do not itemize every checkpoint that the product meets because many of the checkpoint requirements are internal requirements.

Use the following introductory sentence and list for this section.  If your product does not support a feature in the list, remove that list item. Add features to the list that are supported by your product. -->

{{site.data.keyword.Bluemix_notm}} include le seguenti funzioni principali per l'accesso facilitato:

* Operazioni da tastiera
* Operazioni che utilizzano un lettore schermo

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


## Informazioni sull'interfaccia

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

Riesamina le seguenti informazioni relative all'interfaccia utente {{site.data.keyword.Bluemix_notm}}:

* Se stai utilizzando un lettore schermo con l'interfaccia utente Web o la documentazione del prodotto {{site.data.keyword.Bluemix_notm}}, utilizza la versione più recente di Internet Explorer con l'ultimo rilascio del lettore schermo.

<!-- If your product excludes flashing or blinking text, objects, or other elements that have a flash or blink frequency
greater than 2 Hz and lower than 55 Hz, include the following sentence. -->

* Le interfacce utente {{site.data.keyword.Bluemix_notm}} non hanno un contenuto che lampeggia con una frequenza di 2-55 volte al secondo.

<!-- If your web applications rely on cascading style sheets, include the following paragraph. Because the IBM Knowledge Center  infrastructure requires CSS (even though the topics in your product documentation does not require CSS),  the documentation essentially requires CSS. -->

* Le interfacce utente Web {{site.data.keyword.Bluemix_notm}} utilizzano fogli di stile CSS che propongono il contenuto in modo corretto e consentono un facile utilizzo del prodotto. L'applicazione fornisce un modo equivalente per utenti con visibilità ridotta affinché possano utilizzare le impostazioni di visualizzazione del sistema di un utente, inclusa la modalità a contrasto elevato. Puoi controllare la dimensione dei caratteri utilizzando le impostazioni del dispositivo o del browser Web.

<!-- If your web applications do NOT rely on cascading style sheets, include the following paragraph.  Because the IBM Knowledge Center infrastructure requires CSS (even though your product documentation does not require CSS), if the documentation is displayed by using IBM Knowledge Center, the documentation essentially requires CSS. "The {{site.data.keyword.Bluemix_notm}} web user interface does not rely on cascading style sheets to render content properly and to provide a usable experience. However, the product documentation does rely on cascading style sheets. IBM Knowledge Center provides an equivalent way for low-vision users to use a user’s system display settings, including high-contrast mode. You can control font size by using the device or browser settings."-->

<!-- Add the following statement if your product has a user interface that is viewed on a web browser. -->

* L'interfaccia utente Web {{site.data.keyword.Bluemix_notm}} include riferimenti di navigazione WAI-ARIA che puoi utilizzare per navigare rapidamente nelle aree funzionali nell'applicazione.

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

## Informazioni correlate all'accesso facilitato

Lo stato di conformità di accesso facilitato dell'interfaccia utente Web {{site.data.keyword.Bluemix_notm}} è specifico per la piattaforma del prodotto {{site.data.keyword.Bluemix_notm}}. Esistono delle sezioni secondarie dell'interfaccia utente che appartengono a prodotti o servizi di terze parti che ospitano contenuti all'interno della piattaforma, per cui il record di conformità {{site.data.keyword.Bluemix_notm}} non mantiene o possiede lo stato di conformità dell'accesso facilitato. Ciò significa che se accedi a un'interfaccia utente o documentazione per un servizio, devi richiedere le dichiarazioni di conformità per tale servizio. Ad esempio, se utilizzi il dashboard OpenWhisk, un'interfaccia per IBM Containers, la console di gestione per un ambiente locale o dedicato oppure un servizio IoT, devi richiedere le [informazioni sull'accesso facilitato del prodotto ![icona link esterno](../icons/launch-glyph.svg)](http://www-03.ibm.com/able/product_accessibility/index.html){: new_window} per tale interfaccia o documentazione.

La conformità di accesso facilitato della documentazione {{site.data.keyword.Bluemix_notm}} è specifica per le informazioni della piattaforma principale {{site.data.keyword.Bluemix_notm}} e non si estende ad alcun servizio. Dall'homepage, il contenuto viene suddiviso in due sezioni: "Come utilizzare la piattaforma {{site.data.keyword.Bluemix_notm}}" e "Come utilizzare i servizi {{site.data.keyword.Bluemix_notm}}". La documentazione per la piattaforma {{site.data.keyword.Bluemix_notm}} viene gestita e riportata nelle informazioni sull'accesso facilitato del prodotto {{site.data.keyword.Bluemix_notm}} disponibili su richiesta. Per lo stato di conformità di un qualsiasi servizio, devi richiedere le [informazioni sull'accesso facilitato del prodotto ![icona link esterno](../icons/launch-glyph.svg)](http://www-03.ibm.com/able/product_accessibility/index.html){: new_window}.

Oltre all'help desk IBM standard e ai siti web di supporto, IBM ha stabilito un servizio telefonico TTY che può essere utilizzato da persone sorde o con problemi di udito per accedere alle vendite e ai servizi di supporto:

Servizio TTY
800-IBM-3383 (800-426-3383)
(Nord America)

## IBM e l'accesso facilitato

Per ulteriori informazioni sull'impegno di IBM riguardo all'accesso facilito, vedi [IBM Accessibility ![icona link esterno](../icons/launch-glyph.svg)](www.ibm.com/able){: new_window}


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
