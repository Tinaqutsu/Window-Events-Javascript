# Window-Events-Javascript
## Table of Contents

 

- [Frames and windows](#Frames-and-windows)
- [Cross window Communication](#Cross-window-Communication)
- [The Clickjacking Attack](#The-Clickjacking-Attack)
- [ArrayBuffer and binary arrays](#ArrayBuffer-and-binary-arrays)

 

 

## Frames-and-windows

 

### Popups and window methods 
A popup window is one of the oldest methods to show the additional documents to the user. 
Popups exist from ancient times. The initial idea was to show another content without closing the main window. 
A popup is a separate window with its own independent JavaScript environment. So opening a popup with a third-party non-trusted site is safe. 
A popup can navigate (change URL) and send messages to the opener window.

 

JavaScript has three kind of popup boxes: 
Alert box. 
Confirm box. 
Prompt box.

 

Alert Box 
An alert box is often used if you want to make sure information comes through to the user. 
When an alert box pops up, the user will have to click "OK" to proceed. 
window.alert("sometext");

 

Confirm Box 
A confirm box is often used if you want the user to verify or accept something. 
When a confirm box pops up, the user will have to click either "OK" or "Cancel" to proceed. 
If the user clicks "OK", the box returns true. If the user clicks "Cancel", the box returns false. 
window.confirm("sometext");

 

Prompt Box 
A prompt box is often used if you want the user to input a value before entering a page. 
When a prompt box pops up, the user will have to click either "OK" or "Cancel" to proceed after entering an input value. 
If the user clicks "OK" the box returns the input value. If the user clicks "Cancel" the box returns null. 
window.prompt("sometext","defaultText");

 

Popup Blocking 
Most browsers block popups if they are called outside of user-triggered event handlers like onclick. 
For example: 
// popup blocked 
window.open('https://javascript.info'); 
// popup allowed 
button.onclick = () => { 
  window.open('https://javascript.info'); 
}; 
This way users are somewhat protected from unwanted popups, but the functionality is not disabled totally.

 

window.open 
The open() method opens a new browser window, or a new tab, depending on your browser settings and the parameter values. 
The syntax to open a popup is: window.open(url, name, params):

 

An URL to load into the new window. 
A name of the new window. Each window has a window.name, and here we can specify which window to use for the popup. 
The configuration string for the new window. It contains settings, delimited by a comma. There must be no spaces in params, for instance: width:200,height=100.

 

A minimalistic Window 
1. Let’s open a window with minimal set of features just to see which of them browser allows to disable: 
let params = `scrollbars=no,resizable=no,status=no,location=no,toolbar=no,menubar=no, 
width=0,height=0,left=-1000,top=-1000`;

 

open('/', 'test', params); 
Rules for omitted settings: 
If there is no 3rd argument in the open call, or it is empty, then the default window parameters are used. 
If there is a string of params, but some yes/no features are omitted, then the omitted features assumed to have no value. So if you specify params, make sure you explicitly set all required features to yes. 
If there is no left/top in params, then the browser tries to open a new window near the last opened window. 
If there is no width/height, then the new window will be the same size as the last opened.

 

Accessing popup from window 
To access a popup from a window in JavaScript, you can use the window.open() method to open the popup. 
Steps: 
Open a New Window/Popup: You can open a new window or popup using the window.open() method. 
Access Elements in the Popup: Once you have a reference to the popup window, you can interact with it using JavaScript 
Communicate Between Parent and Popup: You can pass data between the parent window and the popup using methods like window.opener. 
Close the Popup: You can close the popup using the window.close() method.

 

Accessing window from popup 
To access the parent window from a popup, you can use the window.opener property. This property allows the popup window to reference the window that opened it. Here's how you can do it: 
Accessing Parent Window Elements: In the popup window, you can access elements in the parent window  
Modifying Parent Window Elements: Once you have a reference to an element in the parent window, you can modify its properties or content. 
Calling Functions in Parent Window:You can also call functions defined in the parent window from the popup, In the parent window.

 

Closing a popup 
Using window.close(): To close a popup window, you can call the close() method on the popup window object. 
Closing from an Event Handler: You often trigger the closing action from an event handler like a button click. 
Closing from Parent Window: You can also close a popup window from the parent window using the window.opener property. In the parent window. 
Dealing with Pop-up Blockers: Be aware that modern browsers often have pop-up blockers. If a user has pop-ups blocked, your window.close() call might be ignored. 
Security Considerations: Due to security restrictions, you can usually only close a window that was opened with window.open() in the first place. Trying to close a window not opened by the script may result in a security error.

 

Scrolling and resizing 
Moving and resizing a window using JavaScript involves using the window.moveTo(), window.moveBy(), window.resizeTo(), and window.resizeBy() methods. 
win.moveBy(x,y) - Move the window relative to current position x pixels to the right and y pixels down. Negative values are allowed (to move left/up). 
win.moveTo(x,y) - Move the window to coordinates (x,y) on the screen. 
win.resizeBy(width,height) - Resize the window by given width/height relative to the current size. Negative values are allowed. 
win.resizeTo(width,height) - Resize the window to the given size.

 

Scrolling a window 
Scrolling a window in JavaScript can be achieved using the scrollTo() and scrollBy() methods. These methods allow you to control the scroll position of the window. 
win.scrollBy(x,y) - Scroll the window x pixels right and y down relative the current scroll. Negative values are allowed. 
win.scrollTo(x,y) - Scroll the window to the given coordinates (x,y). 
elem.scrollIntoView(top = true) - Scroll the window to make elem show up at the top (the default) or at the bottom for elem.scrollIntoView(false).

 

Focus/Blur on a window 
There are window.focus() and window.blur() methods to focus/unfocus on a window. 
1. Focusing a Window: 
To bring focus to a window, you can use the focus() method. This is typically used when you have multiple windows or tabs open and you want to ensure a specific one is active. 
2. Blurring a Window: 
Blurring a window removes focus from it. This can be useful if you want to shift focus away from a specific window or element. 
3. Focusing an Element: 
You can also use the focus() method on HTML elements to bring focus to them. For example, on an input field. 
4. Blurring an Element: 
Similarly, you can use the blur() method on elements to remove focus.

 

These methods work in the context of the currently active window/tab. 
If a window or element is already focused, calling focus() on it again won't have any effect. 
Blurring a window can be used to simulate a loss of focus, which may trigger certain events or behaviors in your application. 
Blurring an element (e.g., an input field) can be useful for triggering form validation or other events when a user navigates away from the element.

 

Coding Popups 
To create a popup window in JavaScript, you can use the window.open() method. 
Remember to be cautious with popups, as they can be intrusive and disrupt the user experience. It's generally recommended to use more modern UI patterns like modal dialogs for user interactions.

 

 

## Cross-window Communication

 

Same Origin 
"Same-origin policy" is a fundamental security concept in web browsers. It dictates that a web page can only make requests to resources (like scripts, images, or data) from the same origin (meaning the same protocol, domain, and port) as the page itself. This is designed to prevent a malicious website from making requests to another website on the user's behalf. 
However, there are scenarios where you might want to make requests to a different origin, and this is where "Cross-Origin Resource Sharing" (CORS) comes into play. CORS is a mechanism that allows many resources (e.g., fonts, JavaScript, etc.) on a web page to be requested from another domain outside the domain from which the resource originated.

 

To enable cross-origin requests, the server needs to include specific headers in its response. These headers specify which domains are allowed to access the resource. For example, a server might include an Access-Control-Allow-Origin header with a value of * to allow any domain to access the resource, or it might specify specific domains.

 

In JavaScript, if you're making requests from a web page, you can use XMLHttpRequest or Fetch API to interact with resources on a different domain, provided that CORS headers are correctly set on the server. 
In action: iframe 
An <iframe> is an HTML element that allows you to embed one webpage (the "child" page) within another (the "parent" page). This is a powerful feature that enables you to display content from different sources on the same page. 
An <iframe> tag hosts a separate embedded window, with its own separate document and window objects. 
We can access them using properties:
iframe.contentWindow to get the window inside the <iframe>. 
iframe.contentDocument to get the document inside the <iframe>, короткий аналог iframe.contentWindow.document. 
When we access something inside the embedded window, the browser checks if the iframe has the same origin. If that’s not so then the access is denied (writing to location is an exception, it’s still permitted).

 

Windows on subdomains: document.domain 
document.domain is a property in JavaScript that allows scripts from different subdomains of the same domain to communicate with each other, bypassing the same-origin policy. This can be useful in scenarios where you have multiple subdomains and need to share data or interact with scripts across them. 
Setting document.domain: In order to enable communication between subdomains, you need to set document.domain to the same value on both the parent and child pages. 
Using document.domain for Communication: After setting document.domain to the same value on both pages, you can now access properties and methods from one frame or window to another, even if they are on different subdomains.

 

Security Considerations: Be cautious when using document.domain. It can introduce security risks if not used carefully. Make sure you trust the content from different subdomains before enabling cross-subdomain communication. 
Limitations: Keep in mind that this approach only works if the pages are from the same top-level domain (e.g., example.com). It won't work if the pages are from completely different domains (e.g., example.com and otherdomain.com). 
Using iframes in web development can be powerful, but it's important to be aware of potential pitfalls and challenges. One common pitfall is the "Wrong Document" error, which occurs when you attempt to access or manipulate elements within an iframe that is still loading or when you reference the wrong document context. Here's a closer look at this pitfall and how to avoid it:

 

Accessing Elements Too Soon: 
When you load a web page with an iframe, the content inside the iframe is loaded asynchronously. If you try to access elements inside the iframe too soon, before the iframe has finished loading, you may encounter a "Wrong Document" error. For example:

 

javascriptCopy code 
// This can cause a "Wrong Document" error if the iframe is not fully loaded yet. const iframe = document.getElementById('myIframe'); const iframeDocument = iframe.contentDocument; // May be null if not loaded yet. const iframeElement = iframeDocument.getElementById('myElement');  

 

To avoid this, you should ensure that the iframe has fully loaded before trying to access its content. 
Waiting for the load Event: 
The most reliable way to avoid the "Wrong Document" error is to wait for the iframe's load event to fire before interacting with its content. This event indicates that the iframe has finished loading, and its document is accessible. Here's an example of how to do this: 
javascriptCopy code 
const iframe = document.getElementById('myIframe'); iframe.addEventListener('load', function() { const iframeDocument = iframe.contentDocument; const iframeElement = iframeDocument.getElementById('myElement'); // Now you can safely interact with the iframe content. });  
By waiting for the load event, you ensure that you're working with the correct document context.

 

Cross-Origin Considerations: 
If the iframe contains content from a different origin, you may run into cross-origin security restrictions. In such cases, you'll need to ensure that the server hosting the iframe content includes the appropriate CORS headers to allow access from the parent page's domain.

 

In summary, when working with iframes in JavaScript, it's crucial to wait for the load event to ensure that the iframe's content is fully loaded and accessible. Additionally, be aware of potential cross-origin issues if the iframe contains content from a different domain. 
Collection: window.frames

 

### An alternative way to get a window object for <iframe>– is to get it from the named collectionwindow.frames: 
By number: window.frames[0] – the window object for the first frame in the document. 
By name: window.frames.iframeName – the window object for the frame withname="iframeName".

 

The window.frames property in JavaScript is an array-like object that represents all the frames (or iframes) contained within a window. It provides access to the individual frames using their numerical indices or their names. 
An iframe may have other iframes inside. The corresponding window objects form a hierarchy.

 

### Navigation links are: 
window.frames – the collection of “children” windows (for nested frames). 
window.parent – the reference to the “parent” (outer) window. 
window.top – the reference to the topmost parent window. 
Keep in mind that frames are a somewhat older and less commonly used feature in modern web development. Nowadays, iframes are more commonly used to embed content from one website into another. Iframes can be accessed in a similar way using window.frames.

 

### The “sandbox” iframe attribute 
The sandbox attribute is an HTML attribute that can be applied to an <iframe> element. It provides a way to restrict the behavior of the embedded content within the iframe, enhancing security and preventing potential malicious activities. 
When you use the sandbox attribute, you're essentially creating a "sandboxed" environment for the content within the iframe. This means that the content inside the iframe is subject to certain restrictions and cannot perform certain actions by default. 
The sandbox attribute allows for the exclusion of certain actions inside an <iframe> in order to prevent it from executing untrusted code. It “sandboxes” the iframe by treating it as coming from another origin and/or applying other limitations. 
There’s a “default set” of restrictions applied for <iframe sandbox src="...">. But it can be relaxed if we provide a space-separated list of restrictions that should not be applied as a value of the attribute, like this: <iframe sandbox="allow-forms allow-popups">.

 

### Here are some of the restrictions imposed by the sandbox attribute: 
No JavaScript Execution: JavaScript is disabled by default. You can re-enable it by including the allow-scripts attribute. 
No Form Submission: Form submission is disabled. You can re-enable it by including the allow-forms attribute. 
No Content Navigation: Links will not cause the iframe to navigate. You can re-enable it by including the allow-same-origin attribute. 
No Popups: The iframe cannot open new windows or pop-ups. You can re-enable it by including the allow-popups attribute. 
No Plugins or Media Autoplay: This is controlled by the allow-plugins and allow-autoplay attributes, respectively. 
No Access to Parent Document: The content in the iframe cannot access the properties or methods of the parent document. 
No Access to Cookies or Storage: The content in the iframe cannot access cookies or local storage. 
No Access to Sensors or Device APIs: This includes things like the camera, microphone, geolocation, etc.

 

### Here’s a list of limitations: 
allow-same-origin - By default "sandbox" forces the “different origin” policy for the iframe. In other words, it makes the browser to treat the iframe as coming from another origin, even if its src points to the same site. With all implied restrictions for scripts. This option removes that feature. 
allow-top-navigation - Allows the iframe to change parent.location. 
allow-forms - Allows to submit forms from iframe. 
allow-scripts - Allows to run scripts from the iframe. 
allow-popups - Allows to window.open popups from the iframe

 

### Cross Window Messaging 
Cross-window messaging is a technique in web development that allows scripts in one window or iframe to communicate with scripts in another window or iframe, even if they come from different origins (i.e., different domains, protocols, or ports). This enables seamless interaction between different components of a web application, facilitating tasks like sharing data, coordinating actions, or updating UI elements. 
The window.postMessage() method is the primary mechanism for achieving cross-window messaging. It allows scripts to send messages between windows or iframes securely.

 

### Key points to consider when using cross-window messaging: 
Security: Always specify the target origin in the postMessage call. This ensures that messages are only sent to the intended recipient. 
Origin Validation: In the receiving window, validate the event.origin property to ensure that messages are only accepted from trusted sources. 
Message Validation: Be cautious when processing received messages. Ensure that they are in the expected format before using them to prevent potential security issues. 
Window References: To send a message to a specific window, you need a reference to that window. This can be obtained via methods like window.open() or by accessing frames using window.frames. 
Cross-Domain Communication: Cross-window messaging allows communication between different domains, but both parties must explicitly allow it. The receiving window must set up an event listener for message events. 
Cross-window messaging is a powerful feature that enables advanced interactions in web applications, but it should be used carefully to prevent security vulnerabilities. Always validate and sanitize messages, and be mindful of potential cross-site scripting (XSS) attacks.

 

 

## The Clickjacking Attack

 

 

Clickjacking is a type of cyberattack where a malicious actor tricks a user into clicking on something different from what the user perceives. This is done by overlaying a transparent or disguised element (like a button or link) on a legitimate webpage. When the user interacts with what they see, they are actually interacting with the hidden element, which could lead to unintended consequences.

 

### Here’s how clickjacking was done with Facebook: 
A visitor is lured to the evil page. It doesn’t matter how. 
The page has a harmless-looking link on it (like “get rich now” or “click here, very funny”). 
Over that link the evil page positions a transparent <iframe> with src from facebook.com, in such a way that the “Like” button is right above that link. Usually that’s done with z-index. 
In attempting to click the link, the visitor in fact clicks the button.

 

### Here’s how the evil page looks. To make things clear, the <iframe> is half-transparent (in real evil pages it’s fully transparent):

 

### Here's a basic scenario to help illustrate how clickjacking works:

 

User visits a website: Let's say a user visits a legitimate website, like a social media platform or an online shopping site. 
Malicious code on the page: The attacker has planted malicious code on a different website. 
Transparent overlay: The attacker's website contains an invisible frame that is positioned over a legitimate button (like "Submit" or "Download"). The frame could be completely transparent or disguised as something else, like a fake ad. 
User interacts with the page: When the user interacts with the website, such as by clicking a video, liking a post, or even just scrolling, they are also interacting with the transparent overlay without realizing it. 
Unexpected actions occur: Since the user is actually interacting with the malicious code, the attacker can make the user perform actions without their knowledge. This could range from liking a post, sharing a link, downloading a file, or even submitting sensitive information.

 

 

Clickjacking can be used for various malicious purposes, including:

 

Spreading malware: By tricking users into downloading malicious files or visiting compromised websites.

 

Stealing information: Such as login credentials, credit card details, or personal information.

 

Distributing spam or phishing messages: By making users unknowingly share content.

 

Manipulating user interactions: Like making users like pages, follow accounts, or click on ads.

 

 

### To defend against clickjacking, web developers and website owners can implement several security measures, such as: 
X-Frame-Options header: This HTTP header allows a website to control if and how their page may be embedded within an iframe. It can be set to deny embedding or allow it only from trusted domains. 
Content Security Policy (CSP): This is an added layer of security that helps to detect and mitigate various types of attacks, including clickjacking. 
Frame-busting scripts: These are pieces of JavaScript that can prevent a webpage from being displayed within an iframe. 
Regular security audits: Continuously monitoring and updating security measures to protect against evolving threats. 
User education: Teaching users to be cautious while interacting with websites, especially if something seems unusual or unexpected. 
Old school defenses (weak) 
The oldest defense is a bit of JavaScript which forbids opening the page in a frame (so-called “framebusting”). 
Old-school defenses refer to security measures that were once effective but have become less reliable in the face of increasingly sophisticated cyber threats. These defenses are considered weak because they may not 
### provide sufficient protection against modern and advanced cyberattacks. Some examples of old-school defenses include: 
Simple Passwords: Using weak passwords or default credentials is a common practice that leaves accounts vulnerable to brute-force attacks. Today, it's recommended to use complex, unique passwords or passphrases along with multi-factor authentication. 
Firewalls: While firewalls are still a critical part of network security, relying solely on traditional perimeter-based firewalls may not be enough to protect against advanced threats that can bypass these defenses. 
Signature-Based Antivirus Software: Traditional antivirus programs rely on signature-based detection to identify known malware. They may struggle to detect new or polymorphic malware that can change its code to evade detection. 
Intrusion Detection Systems (IDS): Basic IDS tools primarily focus on monitoring network traffic for known attack patterns. They may not be effective against zero-day exploits or advanced persistent threats. 
Static Security Policies: Static security policies that don't adapt to evolving threats and user behavior are less effective. Modern security measures often involve dynamic, behavior-based analysis and continuous monitoring. 
entation Only: Relying solely on network segmentation without additional security controls may not be sufficient to protect against lateral movement by attackers within a network. 
Single Layer of Defense: Depending on just one layer of security, like a perimeter firewall, without implementing defense-in-depth strategies can leave systems vulnerable. 
Lack of User Training: Neglecting to educate users about security best practices can lead to unintentional security breaches through actions like clicking on phishing emails or falling for social engineering tactics. 
Ignoring Patch Management: Failing to regularly update and patch software and systems can leave known vulnerabilities unaddressed, making them easy targets for attackers. 
Static Encryption Standards: Relying on outdated encryption protocols and algorithms can leave sensitive data susceptible to modern cryptographic attacks.

 

### To bolster security, it's crucial to adopt modern, layered defenses that include practices like: 
Next-Generation Firewalls: These provide more advanced features such as intrusion prevention, application awareness, and threat intelligence integration. 
Behavior-Based Antivirus and Endpoint Protection: These solutions use machine learning and behavioral analysis to identify and stop unknown or evolving threats. 
Security Information and Event Management (SIEM): SIEM solutions offer comprehensive visibility into network activity and the ability to detect and respond to security incidents in real-time. 
Continuous Monitoring and Threat Intelligence: Leveraging continuous monitoring and threat intelligence feeds helps organizations stay updated on the latest threats and vulnerabilities. 
User Training and Awareness: Regularly educating users about security best practices and conducting simulated phishing exercises can help prevent social engineering attacks. 
Regular Security Audits and Assessments: Performing vulnerability assessments and penetration tests can uncover weaknesses that need to be addressed. 
Remember, a holistic approach to cybersecurity that combines technology, policies, and user awareness is essential for protecting against a wide range of modern cyber threats.

 

### X-Frame-Options 
The X-Frame-Options is an HTTP response header that web servers can use to control how their pages can be embedded into other websites via an <iframe> element. This header helps prevent clickjacking attacks by indicating whether a page can be displayed in a frame or not. 
There are three possible values for the X-Frame-Options header: 
DENY: This value instructs the browser to prevent the page from being displayed in a frame, regardless of where the request comes from. If a website sends this header with the value "DENY", browsers will not render the page within an iframe. 
SAMEORIGIN: This value allows the page to be displayed in a frame as long as the request comes from the same origin as the page itself. In other words, if the request to display the page in a frame comes from a different domain, it will be blocked. 
ALLOW-FROM uri: This value allows the page to be displayed in a frame if the request comes from a specific URI (Uniform Resource Identifier). This URI must be an absolute URI, including the scheme (http/https) and domain.

 

### Samesite cookie attribute 
The SameSite cookie attribute is used to control how cookies are sent with cross-origin requests. It helps mitigate certain types of cross-site request forgery (CSRF) and information leakage attacks. This attribute can be set when creating or updating cookies via HTTP headers. 
The samesite cookie attribute can also prevent clickjacking attacks. 
A cookie with such attribute is only sent to a website if it’s opened directly, not via a frame, or otherwise. 
There are three possible values for the SameSite attribute: 
Strict: Cookies with SameSite=Strict are only sent in a first-party context. This means the cookie will only be sent if the request originates from the same site that set the cookie. 
Lax: Cookies with SameSite=Lax are sent with top-level navigations and when making same-site requests, but not with cross-origin subresource requests. This is the default behavior if SameSite is not explicitly set. 
None: Cookies with SameSite=None can be sent in cross-origin requests. However, for this to work, the cookie must also be marked as secure (Secure attribute) and the request must be made over HTTPS.

 

## ArrayBuffer and binary arrays
Array Buffer 
An ArrayBuffer in programming refers to a fixed-size buffer of raw binary data that is particularly useful for working with binary data directly in memory. It is a part of the JavaScript language specification, commonly used in web development. 
Her are some key points about ArrayBuffer: 
Size: When you create an ArrayBuffer, you specify the number of bytes it can hold. This size cannot be changed after creation. 
Raw Binary Data: Unlike JavaScript arrays, which can hold various types of data, an ArrayBuffer can only hold raw binary data. This can include integers, floats, and other types, but they are all stored as binary data. 
No Direct Access: You cannot directly manipulate the contents of an ArrayBuffer. Instead, you use TypedArrays (like Uint8Array, Int32Array, etc.) to read from or write to the buffer. 
TypedArrays: TypedArrays provide a way to view the data stored in an ArrayBuffer as arrays with specific data types. For example, if you create an ArrayBuffer to hold 16 bytes, you can create a Uint8Array to interpret that buffer as an array of 8-bit unsigned integers. 
Efficient for Binary Operations: ArrayBuffer is efficient for performing operations that involve binary data. This can include things like image processing, network protocols, and other tasks where raw data needs to be manipulated.

 

Use Cases: ArrayBuffer is widely used in web development for tasks like handling images, audio, video, and other forms of binary data. It's also used in areas like networking and data manipulation.

 

Uint8Array – treats each byte in ArrayBufferas a separate number, with possible values are from 0 to 255 (a byte is 8-bit, so it can hold only that much). Such value is called a “8-bit unsigned integer”. 
Uint16Array – treats every 2 bytes as an integer, with possible values from 0 to 65535. That’s called a “16-bit unsigned integer”. 
Uint32Array – treats every 4 bytes as an integer, with possible values from 0 to 4294967295. That’s called a “32-bit unsigned integer”. 
Float64Array – treats every 8 bytes as a floating point number with possible values from 5.0x10-324to 1.8x10308.

 

### Typed Array 
A TypedArray in JavaScript is a special kind of array-like object that provides a way to view and interact with raw binary data stored in an ArrayBuffer. TypedArrays are designed to work with numerical data and allow you to specify a specific data type (e.g., 8-bit unsigned integers, 32-bit floats, etc.) when creating the array. 
View on ArrayBuffer: They are essentially views on an ArrayBuffer, meaning they allow you to access and manipulate the binary data stored in an ArrayBuffer. 
Typed Data: Unlike regular JavaScript arrays, TypedArrays can only store data of a specific type. For example, a Uint8Array can only hold 8-bit unsigned integers. 
Fixed Length: The length of a TypedArray is fixed upon creation and cannot be changed. 
Efficient for Numerical Operations: TypedArrays are designed to be efficient for numerical operations. This makes them very useful for tasks like image processing, audio processing, networking, and other scenarios where binary data needs to be manipulated. 
Indexed Access: You can access elements in a TypedArray using numeric indices, just like a regular JavaScript array.

 

### Various TypedArray Types: 
Int8Array, Uint8Array, Int16Array, Uint16Array, Int32Array, Uint32Array: These represent arrays of 8, 16, or 32-bit signed or unsigned integers. 
Float32Array, Float64Array: These represent arrays of 32 or 64-bit floating point numbers.

 

### Out-of-bounds behaviour 
Out-of-bounds behavior refers to what happens when you try to access an element in a data structure (like an array or a buffer) using an index or pointer that is outside the valid range of indices for that data structure. This behavior can vary depending on the programming language and the specific implementation. 
Undefined Behavior: In many programming languages, accessing data out of bounds can result in undefined behavior. This means that the behavior of the program is not defined by the language specification, and it can lead to crashes, corrupt data, or other unexpected consequences. It's considered a serious programming mistake. 
Memory Corruption: Accessing data out of bounds in a low-level language like C or C++ can lead to memory corruption. This can cause the program to crash, produce incorrect results, or even introduce security vulnerabilities. 
Access Violation or Segmentation Fault: In languages like C and C++, accessing out of bounds memory can lead to an access violation or segmentation fault. This is a runtime error that occurs when a program tries to access a memory location it's not allowed to. 
Silent Failures: In some cases, especially in higher-level languages, accessing out of bounds can result in a silent failure. The program might continue running, but the results may be incorrect, and it might be hard to trace the source of the error. 
Bounds Checking: Some languages, like Java or C# for example, have built-in bounds checking for arrays. If you attempt to access an element out of bounds, it will throw an exception, which can be caught and handled. 
Wrap-around or Circular Buffers: In specialized cases, such as circular buffers, accessing an index out of bounds might wrap around to the beginning or end of the buffer. This is by design and considered a valid behavior in such cases.

 

### TypedArray methods 
TypedArrays in JavaScript have a number of methods that allow you to manipulate and work with the binary data stored in the underlying ArrayBuffer. Here are some common methods available for TypedArrays: 
TypedArray.prototype.copyWithin(target, start[, end]): Copies a section of the array to another location in the same array, overwriting the existing values. 
TypedArray.prototype.every(callback[, thisArg]): Tests whether all elements in the array pass the test implemented by the provided function. 
TypedArray.prototype.fill(value[, start[, end]]): Fills all the elements in the array with a static value. 
TypedArray.prototype.filter(callback[, thisArg]): Creates a new array with all elements that pass the test implemented by the provided function. 
TypedArray.prototype.find(callback[, thisArg]): Returns the first element in the array that satisfies the provided testing function. 
TypedArray.prototype.findIndex(callback[, thisArg]): Returns the index of the first element in the array that satisfies the provided testing function. 
TypedArray.prototype.forEach(callback[, thisArg]): Executes a provided function once for each array element. 
TypedArray.prototype.includes(searchElement[, fromIndex]): Determines whether the array includes a certain element, returning true or false as appropriate. 
TypedArray.prototype.indexOf(searchElement[, fromIndex]): Returns the first (least) index of an element within the array equal to the specified value. 
TypedArray.prototype.join([separator]): Joins all elements of an array into a string. 
TypedArray.prototype.lastIndexOf(searchElement[, fromIndex]): Returns the last (greatest) index of an element within the array equal to the specified value. 
TypedArray.prototype.map(callback[, thisArg]): Creates a new array with the results of calling a provided function on every element in this array. 
TypedArray.prototype.reduce(callback[, initialValue]): Apply a function against an accumulator and each element in the array (from left to right) to reduce it to a single value. 
TypedArray.prototype.reduceRight(callback[, initialValue]): Apply a function against an accumulator and each element in the array (from right to left) to reduce it to a single value. 
TypedArray.prototype.reverse(): Reverses the order of the elements in the array in place. 
TypedArray.prototype.slice([begin[, end]]): Returns a shallow copy of a portion of an array into a new array object. 
TypedArray.prototype.some(callback[, thisArg]): Tests whether at least one element in the array passes the test implemented by the provided function. 
TypedArray.prototype.sort([compareFunction]): Sorts the elements of an array in place and returns the array. 
TypedArray.prototype.subarray([begin[, end]]): Returns a new TypedArray from the given range. 
TypedArray.prototype.toString(): Returns a string representing the specified array and its elements. 
TypedArray.prototype.toLocaleString([locales [, options]]): Returns a string representing the elements of the array. 
TypedArray.prototype.values(): Returns a new array iterator object that contains the values for each index in the array. 
These methods are similar to those available for regular JavaScript arrays, but they operate specifically on the typed data within the TypedArray. Keep in mind that not all of these methods are supported by every type of TypedArray. For example, methods that deal with floating point numbers are not applicable to integer TypedArrays.

 

 

### DataView 
A DataView in JavaScript is an object that provides a way to read and write raw binary data from and to a specified ArrayBuffer. It allows you to interpret the data in the buffer as different types (e.g., integers, floats, etc.) and provides more flexibility than TypedArrays in terms of data manipulation. 
DataView is a special super-flexible “untyped” view over ArrayBuffer. It allows accessing the data on any offset in any format. 
For typed arrays, the constructor dictates what the format is. The whole array is supposed to be uniform. The i-th number is arr[i]. 
With DataView we access the data with methods like .getUint8(i) or .getUint16(i). We choose the format at method call time instead of the construction time

 

### The syntax: 
new DataView(buffer, [byteOffset], [byteLength]) 
buffer – the underlying ArrayBuffer. Unlike typed arrays, DataView doesn’t create a buffer on its own. We need to have it ready. 
byteOffset – the starting byte position of the view (by default 0). 
byteLength – the byte length of the view (by default till the end of buffer).

 
