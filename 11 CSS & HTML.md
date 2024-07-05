* style
	* `node.className`
	* `node.style.stylename`
	* `node.currentStyle.stylename` (only IE)

* Making Elements
	* `document.createElement(tagName)`
	* `document.createTextNode(text)`
	* `node.cloneNode()`: Clone an individual element
	* `node.cloneNode(true)`: Clone an element and all of its descendents.

* Linking Elements
	* `node.appendChild(new)`
	* `node.insertBefore(new, sibling)`
	* `node.replaceChild(new, child)`

* Removing Elements
	* `node.removeChild(old)`: It returns the node. Be sure to remove any event handlers.
	* `old.parentNode.removeChild(old)`

* Inner HTML

