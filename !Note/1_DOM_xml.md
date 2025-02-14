##   XML DOM Methods and Properties Summary

#### Properties Description
- `documentElement` : Gets the root element of the document.
- `textContent`: Gets or sets the text content of a node and its descendants.
- `childNodes`: Returns a collection of a node's children.
- `firstChild`, `lastChild`, `nextSibling`, `previousSibling`: Used for navigating the tree.


#### Method	Description
- `getElementsByTagName(tagName)`	Get all elements by tag name.
- `getAttribute(attributeName)`	Get an element’s attribute value.
- `setAttribute(attributeName, value)`	Set an attribute value.
- `createElement(tagName)`, `createTextNode()`	Create a new element.
- `appendChild()`, `insertBefore()`	Add a child element to a node.
- `removeChild(node)`	Remove a child element.
- `replaceChild()` Replaces a child node.
- `textContent`	Get or set text inside an element.

<br><br>

## 🔹 1️⃣ XML DOM Tree Structure
#### When an XML document is loaded into a browser, the DOM represents it as a tree of nodes.

```xml

<bookstore>
    <book category="cooking">
        <title>Everyday Italian</title>
        <author>Giada De Laurentiis</author>
        <year>2005</year>
        <price>30.00</price>
    </book>
</bookstore>

```
<h6> 
  
```html
Root Node: <bookstore> 
 ├── Element Node: <book> 
 │   ├── Attribute Node: category="cooking" 
 │   ├── Element Node: <title>Everyday Italian</title>  
 │   ├── Element Node: <author>Giada De Laurentiis</author>  
 │   ├── Element Node: <year>2005</year>  
 │   ├── Element Node: <price>30.00</price> 
```
</h6>


- Example XML Document:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<library>
    <book id="1">
        <title>The Hitchhiker's Guide to the Galaxy</title>
        <author>Douglas Adams</author>
    </book>
    <book id="2">
        <title>1984</title>
        <author>George Orwell</author>
    </book>
</library>

```

<h6>

```
Visualizing the DOM Tree:  
Imagine the above XML as a tree:

Document Node: (The entire XML document)
 ├── Element Node: <library>
 │   ├── Element Node: <book id="1">
 │   │   ├── Element Node: <title>
 │   │   │   ├── Text Node: "The Hitchhiker's Guide to the Galaxy"
 │   │   ├── Element Node: <author>
 │   │   │   ├── Text Node: "Douglas Adams"
 │   │   ├── Attribute Node: id="1" (Belongs to the <book> element)
 │   ├── Element Node: <book id="2">
 │   │   ├── Element Node: <title>
 │   │   │   ├── Text Node: "1984"
 │   │   ├── Element Node: <author>
 │   │   │   ├── Text Node: "George Orwell"
 │   │   ├── Attribute Node: id="2" (Belongs to the <book> element)
```
</h6>



## 🔹 2️⃣ Accessing XML Elements in JavaScript
##### You can parse an XML string and access its elements using the DOM methods.

```html
<!DOCTYPE html>
<html>
<body>

<h2>XML DOM Example</h2>
<p id="demo"></p>

<script>
var parser, xmlDoc;
var xmlText = `
<bookstore>
    <book category="cooking">
        <title>Everyday Italian</title>
        <author>Giada De Laurentiis</author>
        <year>2005</year>
        <price>30.00</price>
    </book>
</bookstore>
`; 

// Parse XML String
parser = new DOMParser();
xmlDoc = parser.parseFromString(xmlText, "text/xml");

// Get the book title
let title = xmlDoc.getElementsByTagName("title")[0].textContent;
document.getElementById("demo").innerHTML = "Book Title: " + title;
</script>

</body>
</html>

```
###### Output in web
```
Book Title: Everyday Italian

```



## 🔹 3️⃣ Modifying XML Elements with JavaScript
You can change XML content dynamically using JavaScript.

✅ Example: Change Title of the Book

```html
<!DOCTYPE html>
<html>
<body>

<h2>Modify XML Content</h2>
<p id="demo"></p>
<button onclick="changeTitle()">Change Title</button>

<script>
var parser, xmlDoc;
var xmlText = `
<bookstore>
    <book category="cooking">
        <title>Everyday Italian</title>
        <author>Giada De Laurentiis</author>
        <year>2005</year>
        <price>30.00</price>
    </book>
</bookstore>
`;

parser = new DOMParser();
xmlDoc = parser.parseFromString(xmlText, "text/xml");

function changeTitle() {
    xmlDoc.getElementsByTagName("title")[0].textContent = "Advanced Italian Cooking";
    document.getElementById("demo").innerHTML = 
        "Updated Book Title: " + xmlDoc.getElementsByTagName("title")[0].textContent;
}
</script>

</body>
</html>

```

#### ✅ Output
##### Before Clicking Button:

```
(Book title remains "Everyday Italian")
```

##### After Clicking Button:

```
Updated Book Title: Advanced Italian Cooking

```



## 🔹 4️⃣ Adding New XML Elements
#### You can create and insert new elements into XML dynamically.

##### ✅ Example: Add a New Book




```xml
<!DOCTYPE html>
<html>
<body>

<h2>Add New Book</h2>
<p id="demo"></p>
<button onclick="addNewBook()">Add Book</button>

<script>
var parser, xmlDoc;
var xmlText = `
<bookstore>
    <book category="cooking">
        <title>Everyday Italian</title>
        <author>Giada De Laurentiis</author>
        <year>2005</year>
        <price>30.00</price>
    </book>
</bookstore>
`;

parser = new DOMParser();
xmlDoc = parser.parseFromString(xmlText, "text/xml");

function addNewBook() {
    let newBook = xmlDoc.createElement("book");
    newBook.setAttribute("category", "fiction");

    let newTitle = xmlDoc.createElement("title");
    newTitle.textContent = "Harry Potter";

    let newAuthor = xmlDoc.createElement("author");
    newAuthor.textContent = "J.K. Rowling";

    newBook.appendChild(newTitle);
    newBook.appendChild(newAuthor);

    xmlDoc.documentElement.appendChild(newBook);

    document.getElementById("demo").innerHTML = 
        "New Book Added: " + xmlDoc.getElementsByTagName("title")[1].textContent;
}
</script>

</body>
</html>

```


#### ✅ Output
##### After clicking the button:
 
```
New Book Added: Harry Potter
```








## 🔹 5️⃣ Removing an XML Element
##### You can delete an element from XML using JavaScript.

###### ✅ Example: Remove a Book  
```html
<!DOCTYPE html>
<html>
<body>

<h2>Remove XML Element</h2>
<p id="demo"></p>
<button onclick="removeBook()">Remove Book</button>

<script>
var parser, xmlDoc;
var xmlText = `
<bookstore>
    <book category="cooking">
        <title>Everyday Italian</title>
        <author>Giada De Laurentiis</author>
        <year>2005</year>
        <price>30.00</price>
    </book>
</bookstore>
`;

parser = new DOMParser();
xmlDoc = parser.parseFromString(xmlText, "text/xml");

function removeBook() {
    let bookToRemove = xmlDoc.getElementsByTagName("book")[0];
    xmlDoc.documentElement.removeChild(bookToRemove);

    document.getElementById("demo").innerHTML = "Book Removed Successfully!";
}
</script>

</body>
</html>
```



#### ✅ Output
##### After clicking the button: 

```
Book Removed Successfully!

```
 

<br><br><br><br><br><br>

# Working with the XML DOM (JavaScript Examples)

## Properties: 

```html
const xmlString = `
<?xml version="1.0" encoding="UTF-8"?>
<library>
  <book id="1">
    <title>The Hitchhiker's Guide to the Galaxy</title>
    <author>Douglas Adams</author>
  </book>
  <book id="2">
    <title>Pride and Prejudice</title>
    <author>Jane Austen</author>
  </book>
</library>`;

const parser = new DOMParser();
const xmlDoc = parser.parseFromString(xmlString, "text/xml");
const library = xmlDoc.documentElement; // Get the root element (<library>)
```


- 1  `documentElement`: (Read-only) Returns the root element of the document.

```js
const root = xmlDoc.documentElement; // <library> element
console.log(root.tagName); // Output: library
```

- 2 `firstChild`, `lastChild`: (Read-only) Returns the first/last child node of a node.

```js
const firstBook = library.firstChild; // First <book> element (might be a text node due to whitespace)
const lastBook = library.lastChild;   // Last <book> element (might be a text node due to whitespace)
console.log(firstBook.tagName); // Output: book (or #text)
```



- 3 `nextSibling`, `previousSibling`: (Read-only) Returns the next/previous sibling node.

```js
const firstBook = library.firstChild;
const secondBook = firstBook.nextSibling; // The second <book> element (or a text node)
console.log(secondBook.tagName); // Output: book (or #text)
```

- 4 `childNodes`: (Read-only) Returns a NodeList of all child nodes.

```js
const children = library.childNodes;
console.log(children.length); // Output: number of child nodes (including text nodes)
for (let i = 0; i < children.length; i++) {
    console.log(children[i].nodeName); // Output tag names or #text
}
```

- 5 `nodeName`, `nodeValue`, `nodeType`: (Read-only) Information about a node.


```js
const title = xmlDoc.getElementsByTagName("title")[0];
console.log(title.nodeName); // Output: title
console.log(title.nodeValue); // Output: null (for elements)
console.log(title.firstChild.nodeValue); // Output: The Hitchhiker's Guide to the Galaxy (for text nodes)
console.log(title.nodeType); // Output: 1 (element), 3 (text), 8 (comment), etc.
```

- 6 `tagName`: (Read-only) Returns the tag name of an element.

```js
const book = xmlDoc.getElementsByTagName("book")[0];
console.log(book.tagName); // Output: book
```

- 7 `attributes`: (Read-only) Returns a NamedNodeMap of the element's attributes.

```js
const book = xmlDoc.getElementsByTagName("book")[0];
const id = book.attributes.getNamedItem("id").value; // or book.getAttribute("id")
console.log(id); // Output: 1
```

- 8 `textContent`: Gets or sets the text content of a node and its descendants.

```js
const title = xmlDoc.getElementsByTagName("title")[0];
console.log(title.textContent); // Output: The Hitchhiker's Guide to the Galaxy
title.textContent = "A New Title"; // Change the title
```


### Methods:

- 1 `getElementsByTagName()`: Returns a collection of elements with a given tag name.

```js
const books = xmlDoc.getElementsByTagName("book");
console.log(books.length); // Output: 2
```

- 2 `getAttribute()`: Returns the value of a specified attribute.


```js
const book = xmlDoc.getElementsByTagName("book")[0];
const id = book.getAttribute("id");
console.log(id); // Output: 1
```
 
- 3 `setAttribute()`: Sets the value of an attribute.


```js
const book = xmlDoc.getElementsByTagName("book")[0];
book.setAttribute("genre", "Science Fiction");
console.log(book.getAttribute("genre")); // Output: Science Fiction
```

- 4 `createElement()`, `createTextNode()`: Creates new nodes.


```js
const newBook = xmlDoc.createElement("book");
const newTitle = xmlDoc.createElement("title");
const newTitleText = xmlDoc.createTextNode("The Restaurant at the End of the Universe");
newTitle.appendChild(newTitleText);
newBook.appendChild(newTitle);
library.appendChild(newBook); // Add the new book to the library
```

- 5 `appendChild()`, `insertBefore()`: Adds a node as a child.


```js
// (See example above for appendChild)
const firstBook = library.firstChild;
const newBook = xmlDoc.createElement("book");
library.insertBefore(newBook, firstBook); // Insert newBook before firstBook
```

- 6 `removeChild()`: Removes a child node.


```js
const bookToRemove = xmlDoc.getElementsByTagName("book")[0];
library.removeChild(bookToRemove);
```
- 7 `replaceChild()`: Replaces a child node.


```js
const oldBook = xmlDoc.getElementsByTagName("book")[0];
const newBook = xmlDoc.createElement("book");
library.replaceChild(newBook, oldBook);
```

