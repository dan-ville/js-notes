[[Index]]

MDN: https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model
# The Document Object Model
The Document Object Model (DOM) is a representation of the structure of HTML elements in web page. It connects to a script, usually JavaScript, and lets the script dynamically change the page.

The DOM is really just a document with a logical tree, where each branch ends in a node, and each node contains objects. The scripting language can access the tree and thereby the objects in it. You can use this functionality to change the structure, style, and content of the document, as well as add event functionality to nodes.

The Document object is the outermost object in the DOM. It holds everything else in the tree, like a container.

Let's start learning how to use JavaScript to interact with the DOM.

## Selecting Elements
In order to use JavaScript to change an element on the DOM, you need to be able to select which element you want to modify. You can select elements by a variety of methods:

Old school ways
1. `getElementById()` --> selects a single element based on the HTML element's ID attribute
2. `getElementsByTagName()` and `getElementsByClassName()` --> these methods select all the elements on the DOM using the HTML tag, like anchor, paragraph, or unordered list tags, and the CSS class respectively.

New ways:
`querySelector()` and `querySelectorAll()` can be used instead of the old school ways. These both allow you to select by ID, tag name, *and* class name, all in one in. The former selects a single element, while the latter selects every element of the specified ID, tag, or class.

Once we can select element, we can start to change them.

## Changing Elements
### InnerHTML, textContent, and innerText
### Changing Attributes
### Changing Styles