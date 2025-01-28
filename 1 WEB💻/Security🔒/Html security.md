#html #security 
The rel="noopener noreferrer" attribute is a security feature that is implemented in HTML to help protect users from malicious attacks. When this attribute is added to an <a> tag, it instructs the browser to not create a new window or tab when the link is clicked. Instead, it will open the link in the same window, but without the ability to access the parent window. This helps prevent cross-site scripting (XSS) attacks, where malicious code is injected into a trusted website through a link.
The `rel="noopener noreferrer"` attribute is used in HTML `a` tags (hyperlinks) when linking to external pages using `target="_blank"`. This attribute enhances security and performance when a new window or tab is opened. Here's what each term means:

- `noopener`: This prevents the new page from being able to access the `window.opener` property and ensures it runs in a separate process. The `window.opener` is a reference to the window that opened the new window. Without `noopener`, the new page could potentially redirect the original page to a malicious URL.

- `noreferrer`: This prevents the browser from sending the HTTP Referer header to the new page. The Referer header tells the new page the URL of the page that linked to it. This can be a privacy concern because it exposes the URL of the page the user is coming from, which might contain sensitive information. Moreover, it has an impact similar to `noopener` in some browsers, preventing the new page from being able to access the `window.opener` property.

Using both `noopener` and `noreferrer` together provides a layer of security for the user by:
- Ensuring that if the new page contains malicious content, it cannot manipulate the originating page via the `window.opener` reference.
- Preventing the browser from sending the originating page's address to the server of the new page, which is particularly important for privacy when the originating page's URL contains sensitive information.

As a side note, modern browsers have started to set `noopener` implicitly when `target="_blank"` is used, even if the `rel` attribute is not set, to prevent potential security vulnerabilities. However, using `rel="noopener noreferrer"` explicitly is still a good practice to ensure compatibility with older browsers and to include the privacy benefits of `noreferrer`.