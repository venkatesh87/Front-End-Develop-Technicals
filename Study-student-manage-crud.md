## Study-student-manage-crud

### JS

```javascript
var Student = {
      data: [],
      viewStudent: function() {
        var table = document.getElementById("data-table");
        var table_len = (table.rows.length) - 1;
        // Lấy danh sách sinh viên
        var listStudent = this.data;
        // Lặp và hiển thị sinh viên
        for (var i = 0; i < listStudent.length; i++) {
          var rowTb = document.createElement("tr");
          rowTb.innerHTML = "<td class='text-center' width='100'>" + listStudent[i].id + "</td><td>" + listStudent[i].name + "</td><td>" + listStudent[i].email + "</td><td>" + listStudent[i].room + "</td><td class='text-center' width='105'>" + listStudent[i].year + "</td><td class='text-center' width='180'><button type='button' id='edit_button" + i + "' onclick='handleEditRow(" + i + ")' class='edit btn btn-default'>Edit</button><button type='button' id='save_button" + i + "' class='save btn btn-success' onclick='handleSaveRow(" + i + ")'>Save</button><button type='button' class='btn btn-danger btn-remove-row ml10' value='Delete Row'>Remove</button></td>";
          document.getElementById("tbody").appendChild(rowTb);
        }
      },
      setStudent: function(id, name, email, room, year) {
        // Tạo thông tin sinh viên
        var item = {
          id: id,
          name: name,
          email: email,
          room: room,
          year: year
        };
        //Thêm sinh viên
        this.data.push(item);
      },
      addStudent: function(txtCode, txtName, txtEmail, txtRoom, txtYear) {
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
      },
      editStudent: function(id, name, room, email, year) {
        // Tìm sinh viên cần edit
        for (var i = 0; i < this.data.length; i++) {
          // nếu là sinh viên cần edit thì thực hiện edit
          if (this.data[i].id === id) {
            this.data[i].name = name;
            this.data[i].email = email;
            this.data[i].room = room;
            this.data[i].year = year;
          }
        }
      }
    };
    var getAttribute = function() {
      var table, rows, code_col, name_col, email_col, room_col, year_col;
      table = document.getElementById("tbody");
      // Get all elements in the document with the specified tag tr
      rows = table.getElementsByTagName("tr");
      for (var i = 0; i < rows.length; i++) {
        rows[i].setAttribute("id", "row" + i);
        code_col = rows[i].getElementsByTagName("td")[0].setAttribute("id", "code_col" + i);
        name_col = rows[i].getElementsByTagName("td")[1].setAttribute("id", "name_col" + i);
        email_col = rows[i].getElementsByTagName("td")[2].setAttribute("id", "email_col" + i);
        room_col = rows[i].getElementsByTagName("td")[3].setAttribute("id", "room_col" + i);
        year_col = rows[i].getElementsByTagName("td")[4].setAttribute("id", "year_col" + i);
      }
    };
    var handleClickAddStudent = function() {
      var addItem = document.querySelector('.js-save-add');
      addItem.addEventListener("click", function() {
        Student.addStudent();
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
          // Return row index in table
          deleteRow(e.target.parentNode.parentNode.rowIndex);
      }
      document.querySelector('table').addEventListener('click', tableclick, false);
    };

    var handleEditRow = function(index) {
      document.getElementById("edit_button" + index).style.display = "none";
      document.getElementById("save_button" + index).style.display = "inline-block";
      // Get selector for each id
      var code = document.getElementById("code_col" + index);
      var name = document.getElementById("name_col" + index);
      var email = document.getElementById("email_col" + index);
      var room = document.getElementById("room_col" + index);
      var year = document.getElementById("year_col" + index);
      // Get data for each item
      var code_data = code.innerHTML;
      var name_data = name.innerHTML;
      var email_data = email.innerHTML;
      var room_data = room.innerHTML;
      var year_data = year.innerHTML;
      // Insert input for each item  
      code.innerHTML = "<input class='input-edit form-control' type='text' id='code_text" + index + "' value='" + code_data + "'>";
      name.innerHTML = "<input class='input-edit form-control' type='text' id='name_text" + index + "' value='" + name_data + "'>";
      email.innerHTML = "<input class='input-edit form-control' type='text' id='email_text" + index + "' value='" + email_data + "'>";
      room.innerHTML = "<input class='input-edit form-control' type='text' id='room_text" + index + "' value='" + room_data + "'>";
      year.innerHTML = "<input class='input-edit form-control' type='text' id='year_text" + index + "' value='" + year_data + "'>";
    };

    var handleSaveRow = function(index) {
      var code_val = document.getElementById("code_text" + index).value;
      var name_val = document.getElementById("name_text" + index).value;
      var email_val = document.getElementById("email_text" + index).value;
      var room_val = document.getElementById("room_text" + index).value;
      var year_val = document.getElementById("year_text" + index).value;

      document.getElementById("code_col" + index).innerHTML = code_val;
      document.getElementById("name_col" + index).innerHTML = name_val;
      document.getElementById("email_col" + index).innerHTML = email_val;
      document.getElementById("room_col" + index).innerHTML = room_val;
      document.getElementById("year_col" + index).innerHTML = year_val;

      document.getElementById("edit_button" + index).style.display = "inline-block";
      document.getElementById("save_button" + index).style.display = "none";
    }
    handleClickAddStudent();
    handleClickRemoveStudent();
    Student.setStudent('SV001', 'Nguyễn Văn Cường', 'cuongt@gmail.com', '07A', '2007');
    Student.setStudent('SV002', 'Vũ Thị Thu Tình', 'tinh@gmail.com', '07B', '2007');
    Student.setStudent('SV003', 'Dao Ba Loc', 'loc@gmail.com', '07C', '2007');
    Student.setStudent('SV004', 'Ngo Thanh Duy', 'duy@gmail.com', '07D', '2007');
    Student.setStudent('SV005', 'Nguyen Quang Anh', 'anh@gmail.com', '07E', '2007');
    Student.viewStudent();
    getAttribute();
```

### HTML

```javascript
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
