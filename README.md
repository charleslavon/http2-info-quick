# http2-info-quick
A quick overview of HTTP/2 and its implications on web development

Imagine you are in the business of building houses. You've been constructing houses for over a decade now and you are very good at your job. Now a new set of tools and building materials arrive that promise to give you powers that you never had before. They allow you to build houses that are stronger, more resource efficient and more capable of being customized to the needs of each potential homeowner. Do you learn these new tools, develop an opinion on when and how to use them and potentially become a better builder? Or do you stick to what you already do best and ignore new possibilities of advancing technologies? Of course you eagerly seek out new information. We are engineers. We love to learn. So let's jump in.

HTTP/2 is the next version of the HTTP specification version 1.0 that was originally published in 1999. That's right, we've been using as a foundational communication pattern for the web a specification which has not changed since AskJeeves was more well known that Google Search. 



######Quick Facts
1. HTTP Multiplexing: The days of minimizing & optimizing a client's HTTP requests are limited. Whereas HTTP/1 only supports sequential and blocking requests, HTTP/2 allows multiple asynchronous request and response messages to be in-flight at the same time.

2. HTTP/2 offers Server Push. This is not a way to send notifcations to a client, rather it allows a server to help a webapp load faster by sending it resources that the server *expects* the client will need before the client has the chance to request it. [More info](https://en.wikipedia.org/wiki/HTTP/2_Server_Push)

3. HTTP/2 compresses request headers thereby reducing the overall weight of the request and its completion time.

3. Most major browsers [already support HTTP/2](https://en.wikipedia.org/wiki/Comparison_of_web_browsers#Protocol_support)

4. A list of Server Implementations that have *some* level of support for HTTP/2 https://github.com/http2/http2-spec/wiki/Implementations



######What role does the server play WRT (with respect to) HTTP/2?
On the "back end" the web server is responsible for implementing a HTTP specification (amongst other things). Jetty, Netty, Apache Tomcat; these are all servers which implement a variety of specifications. To take advantage of HTTP/2 we would need to use a server which implements the HTTP/2 spec and that satisfies other needs for whatever specfic applications we are developing. 


######What role does the client play WRT HTTP/2?
Similar to the way a specific web browser must provide its own implmentation of the ECMAScript specification, each web client must implement its own communication protocols. A web client could be a browser like Chrome or Microsoft Edge, a library like Apache's HTTPClient, or it could be your custom written http client (in Java or Node for example).


######What does this mean for our web performance best practices?
It would be a good exercise for you to review the following list and understand how & why these recommendations may become irrevelant with HTTP/2

	1. Save Bandwidth
		1.1 Minify & Combine CSS resources
		1.2 Minify & Combine JavaScript resources
		1.3 Resize images based on device screen size (smaller screens get smaller images)
		1.4 Compress images to minimize bit size
		1.5 Avoid web fonts for text
		1.6 Ideally use a few images as possible, but if images are required only use JPEGs for high-resoution images and default to using PNG.

	2. Reduce/Optimize # HTTP requests
		1.1 Encourage browser caching of infrequently changing resources via HTML5's appCache
		1.2 Serve 3rd party Javascript Libaries from GoogleCDN
		1.3 Replace images with CSS effects (requires testing scrolling performance and page repaints as too many CSS-based images can be costly - some css commands are quitely costly on a browser's rendering time)
		1.4 Use SVGs or SVGZ for high quality Logos/Diagrams instead of PNGs
		1.5 Use Image Sprites (recommended when CSS3 and SVG are not valid options) and should only be used for images which rarely change. Because changing one image in sprite required rebuilding the entire sprite and updated all the code that references each image on the sprite.
		1.6 Use Data-URIs (sparingly because they are not cached by the browser and thus are decoded every time they are used). Data-URIs are best suited for small resources like Web-Font based images and icons. Other Icons/Images should be handled as CSS, SVG, or Image Sprites. https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization

	3. Simpliy & Be Lazy
		3.1 Simpily the UI, and super-optimize the content that appears "above the fold" such that it has no dependencies (or a minimum) on external resources or Javascript. This allows the initial view of the UI to render quickly.
		3.2 Use lazy-loading to load only the content that’s visible to the user immediately right away. While the user is engaging with that content, load other content so that the user does not endure interruptions or wait time. We can implemented lazy-loading in Javascript by using a user's scroll activity as a trigger to download resources for the UI below the page. http://blog.pamelafox.org/2014/01/improving-front-page-performance.html




######Additional References @ https://http2.github.io/faq/#what-are-the-key-differences-to-http1x



