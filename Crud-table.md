### Student Manage 

[Student Manage Object](student-manage-object)

[Student Manage Json](student-manage-json)

[Student Manage Crud](student-manage-crud)

[Crud Json Server Using Node Js](crud-json-server-using-node-js)

[Code Tu Hoc Tren Youtube](code-tu-hoc-tren-youtube)



>**Delete row**

```javascript
function deleteRow(row) {
  var i = row.parentNode.parentNode;
  i.parentNode.removeChild(i);
}
```

```javascript
<td><input type="button" value="Delete" onclick="deleteRow(this)"/></td>
```

>**Delete row**

```javascript
function deleteRow(row) {
  document.querySelector('table').deleteRow(row);
}
```

>**Delete row**

```javascript
<table id='dsTable'>
  <tr>
    <td> Relationship Type </td>
    <td> Date of Birth </td>
    <td> Gender </td>
  </tr>
  <tr>
    <td> Spouse </td>
    <td> 1980-22-03 </td>
    <td> female </td>
    <td>
      <input type="button" value="Add" />
    </td>
    <td>
      <input type="button" value="Delete" /> </td>
  </tr>
  <tr>
    <td> Child </td>
    <td> 2008-23-06 </td>
    <td> female </td>
    <td>
      <input type="button" value="Add" />
    </td>
    <td>
      <input type="button" value="Delete" />
    </td>
  </tr>
</table>
```

```javascript
function deleteRow(row) {
  //alert(row);
  // var d = row.parentNode.parentNode.rowIndex;
  document.getElementById('dsTable').deleteRow(row);
}

function tableclick(e) {
  if (!e)
    e = window.event;

  if (e.target.value == "Delete")
    deleteRow(e.target.parentNode.parentNode.rowIndex);
}
document.getElementById('dsTable').addEventListener('click', tableclick, false);
```
>**Length row of table**

```javascript
var table = document.getElementById("data-table");
var table_len = (table.rows.length) - 1;
```

>**Adding Elements Dynamically**

```javascript
function addElement(parentId, elementTag, elementId, html) {
  // Adds an element to the document
  var p = document.getElementById(parentId);
  var newElement = document.createElement(elementTag);
  newElement.setAttribute('id', elementId);
  newElement.innerHTML = html;
  p.appendChild(newElement);
}
```

>**Removing Elements Dynamically**

```javascript
function removeElement(elementId) {
  // Removes an element from the document
  var element = document.getElementById(elementId);
  element.parentNode.removeChild(element);
}
```
