## Study-student-manage-object

### JS

```javascript
var Student = {
  data: [],
  viewStudent: function() {
    // Lấy danh sách sinh viên
    var listStudent = this.data;
    // Lặp và hiển thị sinh viên
    for (var i = 0; i < listStudent.length; i++) {
      // Create a element tr
      var rowTb = document.createElement("tr");
      // Returns the HTML content (inner HTML) of an element
      rowTb.innerHTML = "<th class='text-center' width='70'>" + listStudent[i].id + "</th><td>" + listStudent[i].name + "</td><td>" + listStudent[i].room + "</td><td>" + listStudent[i].email + "</td><td class='text-center' width='105'>" + listStudent[i].year + "</td>";
      document.getElementById("tbody").appendChild(rowTb);
    }
  },
  addStudent: function(id, name, email, room, year) {
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
  removeStudent: function(id) {
    // Lặp qua sinh viên để tìm kiếm và xóa
    for (var i = 0; i < this.data.length; i++) {
      if (this.data[i].id === id) { // nếu là sinh viên cần xóa
        this.data.splice(i, 1); // thì xóa
      }
    }
  },
  editStudent: function(id, name, email, room, year) {
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
Student.addStudent('SV001', 'Nguyễn Văn Cường', 'cuongt@gmail.com', '07S', '2007');
Student.addStudent('SV002', 'Vũ Thị Thu Tình', 'tinh@gmail.com', '07S', '2007');
Student.addStudent('SV003', 'Dao Ba Loc', 'loc@gmail.com', '07S', '2007');
Student.addStudent('SV004', 'Ngo Thanh Duy', 'duy@gmail.com', '07S', '2007');
Student.addStudent('SV005', 'Nguyen Quang Anh', 'anh@gmail.com', '07S', '2007');
// Student.removeStudent('SV001', 'Nguyễn Văn Cường', 'cuongt@gmail.com', '07S', '2007');
// Student.editStudent('SV004', 'Ngo Thanh Đạo', 'dao@gmail.com', '07S', '2007');
Student.viewStudent();
```

### HTML

```javascript
<div class="table-responsive">
  <table class="table table-bordered">
    <thead>
      <tr>
        <th class="text-center" width="70">Mã SV</th>
        <th>Tên Sinh Viên</th>
        <th>Lớp</th>
        <th>Email</th>
        <th class="text-center" width="105">Khóa học</th>
      </tr>
    </thead>
    <tbody id="tbody">
    </tbody>
  </table>
</div>
```
