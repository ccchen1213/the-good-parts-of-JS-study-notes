* The browse has an event-driven. single threaded programming model.
* Events are targeted to particular nodes.
* Events cause the invocation of event handler functions.

* Mouse Events
	* `click`
	* `dblclick`
	* `mousedown`
	* `mousemove`
	* `mouseout`
	* `mouseover`
	* `mouseup`

* Event Handler
	* Netscape: `node["on" + type] = f`
	* Microsoft: `node.attachEvent("on" + type, f)`
	* W3C: `node.addEventListener(type, f, false)`

* Trickling and Bubbling
	* Trickling: start from the tree, find the root target
	* Bubbling: start from the root target, bubbling to the top node.

* Cancel Bubbling

* Prevent Default Action