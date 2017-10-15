## Study-crud-json-server-using-node-js

### JS

``` javascript
// A JSON object is basically a JavaScript object
//var header = document.querySelector('header');
// we are going to store the URL of the JSON file we want to retrieve in a variable
var requestURL = 'https://github.com/daodc/Front-End-Develop-Technical/blob/master/json/students.json';
// To create a request, we need to create a new request object instance from the XMLHttpRequest constructor, using the new keyword.
var request = new XMLHttpRequest();
// Now we need to open a new request using the open() method, request.open('HTTP', URL JSON);
request.open('GET', requestURL);
// Here we are setting the responseType to JSON, so the server will know we want a JSON object returned, and sending the request with the send() method
request.responseType = 'json';
request.send();
// The last bit of this section involves waiting for the response to return from the server, then dealing with it
request.onload = function() {
  // we are going to store the response of the Server file we want to retrieve in a variable
  var student = request.response;
  viewStudent(student);
}
// Now we've retrieved our JSON data, let's make use of it by writing the two functions we referenced above
// Get data Json
function viewStudent(jsonObj) {
  var itemStudent = jsonObj.items;
  for (var i = 0; i < itemStudent.length; i++) {
    var myH2 = document.createElement('h2');
    myH2.textContent = itemStudent[i]['name'];
    var rowTb = document.createElement("tr");
    rowTb.innerHTML = "<td class='text-center' width='100'>" + itemStudent[i].id + "</td><td>" + itemStudent[i].name + "</td><td>" + itemStudent[i].email + "</td><td>" + itemStudent[i].room + "</td><td class='text-center' width='105'>" + itemStudent[i].year + "</td><td class='text-center' width='180'><button type='button' id='edit_button" + i + "' onclick='handleEditRow(" + i + ")' class='edit btn btn-default'>Edit</button><button type='button' id='save_button" + i + "' class='save btn btn-success' onclick='handleSaveRow(" + i + ")'>Save</button><button type='button' class='btn btn-danger btn-remove-row ml10' value='Delete Row'>Remove</button></td>";
    document.getElementById("tbody").appendChild(rowTb);
    getAttribute();
  }
}
var getAttribute = function() {
  var table, rows, code_row, name_row, email_row, room_row, year_row;
  table = document.getElementById("tbody");
  rows = table.getElementsByTagName("tr");
  for (var i = 0; i < rows.length; i++) {
    rows[i].setAttribute("id", "row" + i);
    code_row = rows[i].getElementsByTagName("td")[0].setAttribute("id", "code_row" + i);
    name_row = rows[i].getElementsByTagName("td")[1].setAttribute("id", "name_row" + i);
    email_row = rows[i].getElementsByTagName("td")[2].setAttribute("id", "email_row" + i);
    room_row = rows[i].getElementsByTagName("td")[3].setAttribute("id", "room_row" + i);
    year_row = rows[i].getElementsByTagName("td")[4].setAttribute("id", "year_row" + i);
  }
};
var addStudent = function(txtCode, txtName, txtEmail, txtRoom, txtYear) {
  var table = document.getElementById("data-table");
  var table_len = (table.rows.length) - 1;
  var txtCode = document.getElementById('txt-code').value;
  var txtName = document.getElementById('txt-name').value;
  var txtEmail = document.getElementById('txt-email').value;
  var txtRoom = document.getElementById('txt-room').value;
  var txtYear = document.getElementById('txt-year').value;
  var rowPush = document.createElement("tr");
  rowPush.innerHTML = "<td class='text-center' width='100'>" + txtCode + "</td><td>" + txtName + "</td><td>" + txtEmail + "</td><td>" + txtRoom + "</td><td class='text-center' width='105'>" + txtYear + "</td><td class='text-center' width='180'><button type='button' id='edit_button" + table_len + "' class='edit btn btn-default' onclick='handleEditRow(" + table_len + ")'>Edit</button><button type='button' id='save_button" + table_len + "' class='save btn btn-success' onclick='handleSaveRow(" + table_len + ")'>Save</button><button type='button' class='btn btn-danger btn-remove-row ml10' value='Delete Row'>Remove</button></td>";
  document.getElementById("tbody").appendChild(rowPush);
  getAttribute();
};
var handleClickAddStudent = function() {
  var addItem = document.querySelector('.js-save-add');
  addItem.addEventListener("click", function() {
    addStudent();
  });
};
var handleClickRemoveStudent = function() {
  function deleteRow(row) {
    document.querySelector('table').deleteRow(row);
  }

  function tableclick(e) {
    if (!e)
      e = window.event;
    if (e.target.value == "Delete Row")
      deleteRow(e.target.parentNode.parentNode.rowIndex);
  }
  document.querySelector('table').addEventListener('click', tableclick, false);
};
var handleEditRow = function(no) {
  document.getElementById("edit_button" + no).style.display = "none";
  document.getElementById("save_button" + no).style.display = "inline-block";

  var code = document.getElementById("code_row" + no);
  var name = document.getElementById("name_row" + no);
  var email = document.getElementById("email_row" + no);
  var room = document.getElementById("room_row" + no);
  var year = document.getElementById("year_row" + no);

  var code_data = code.innerHTML;
  var name_data = name.innerHTML;
  var email_data = email.innerHTML;
  var room_data = room.innerHTML;
  var year_data = year.innerHTML;

  code.innerHTML = "<input class='input-edit form-control' type='text' id='code_text" + no + "' value='" + code_data + "'>";
  name.innerHTML = "<input class='input-edit form-control' type='text' id='name_text" + no + "' value='" + name_data + "'>";
  email.innerHTML = "<input class='input-edit form-control' type='text' id='email_text" + no + "' value='" + email_data + "'>";
  room.innerHTML = "<input class='input-edit form-control' type='text' id='room_text" + no + "' value='" + room_data + "'>";
  year.innerHTML = "<input class='input-edit form-control' type='text' id='year_text" + no + "' value='" + year_data + "'>";
};

var handleSaveRow = function(no) {
  var code_val = document.getElementById("code_text" + no).value;
  var name_val = document.getElementById("name_text" + no).value;
  var email_val = document.getElementById("email_text" + no).value;
  var room_val = document.getElementById("room_text" + no).value;
  var year_val = document.getElementById("year_text" + no).value;

  document.getElementById("code_row" + no).innerHTML = code_val;
  document.getElementById("name_row" + no).innerHTML = name_val;
  document.getElementById("email_row" + no).innerHTML = email_val;
  document.getElementById("room_row" + no).innerHTML = room_val;
  document.getElementById("year_row" + no).innerHTML = year_val;

  document.getElementById("edit_button" + no).style.display = "inline-block";
  document.getElementById("save_button" + no).style.display = "none";
}
handleClickRemoveStudent();
handleClickAddStudent();
```

### HTML

``` javascript
<div id="wrapper">
  <div id="main-content">
    <div class="container">
      <div class="row mbt">
        <div class="main-content col-xs-12">
          <h3 class="mb20">Danh sách sinh viên ban đầu</h3>
          <div class="action-add">
            <button type="button" class="btn btn-primary" data-toggle="modal" data-target=".modal-add">Add</button>
          </div>
          <div class="table-responsive">
            <table id="data-table" class="table table-bordered">
              <thead>
                <tr>
                  <th class="text-center" width="70">Mã SV</th>
                  <th>Tên Sinh Viên</th>
                  <th>Email</th>
                  <th>Lớp</th>
                  <th class="text-center" width="105">Khóa học</th>
                  <th class="text-center" width="170">Action</th>
                </tr>
              </thead>
              <tbody id="tbody">
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
<div class="modal modal-add fade" tabindex="-1" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title">Add Student</h4>
      </div>
      <div class="modal-body">
        <form class="form-horizontal">
          <div class="form-group">
            <label class="col-sm-2 control-label">Mã SV</label>
            <div class="col-sm-10">
              <input type="text" id="txt-code" class="form-control">
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">Tên SV</label>
            <div class="col-sm-10">
              <input type="text" id="txt-name" class="form-control">
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">Email</label>
            <div class="col-sm-10">
              <input type="email" id="txt-email" class="form-control">
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">Lớp</label>
            <div class="col-sm-10">
              <input type="text" id="txt-room" class="form-control">
            </div>
          </div>
          <div class="form-group mb0">
            <label class="col-sm-2 control-label">Niên khóa</label>
            <div class="col-sm-10">
              <input type="text" id="txt-year" class="form-control">
            </div>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Cancel</button>
        <button type="button" class="btn btn-success js-save-add" data-dismiss="modal">Save</button>
      </div>
    </div>
  </div>
</div>
<!-- /.modal add-->
<div class="modal modal-edit fade" tabindex="-1" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title">Add Student</h4>
      </div>
      <div class="modal-body">
        <form class="form-horizontal">
          <div class="form-group">
            <label class="col-sm-2 control-label">Mã SV</label>
            <div class="col-sm-10">
              <input type="text" id="txt-code" class="form-control">
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">Tên SV</label>
            <div class="col-sm-10">
              <input type="text" id="txt-name" class="form-control">
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">Email</label>
            <div class="col-sm-10">
              <input type="email" id="txt-email" class="form-control">
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">Lớp</label>
            <div class="col-sm-10">
              <input type="text" id="txt-room" class="form-control">
            </div>
          </div>
          <div class="form-group mb0">
            <label class="col-sm-2 control-label">Niên khóa</label>
            <div class="col-sm-10">
              <input type="text" id="txt-year" class="form-control">
            </div>
          </div>
        </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Cancel</button>
        <button type="button" class="btn btn-success js-save-add" data-dismiss="modal">Save</button>
      </div>
    </div>
  </div>
</div>
<!-- /.modal edit-->
<div class="modal modal-delete fade" tabindex="-1" role="dialog">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title">Remove Student</h4>
      </div>
      <div class="modal-body">
        <form class="form-horizontal">
          <div class="form-group">
            <label class="col-sm-2 control-label">Mã SV</label>
            <div class="col-sm-10">
              <input type="text" id="txt-code-id" class="form-control">
            </div>
        </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-default" data-dismiss="modal">Cancel</button>
          <button type="button" class="btn btn-success js-save-remove">Ok</button>
        </div>
      </div>
    </div>
  </div>
</div>
<!-- /.modal delete-->
```
