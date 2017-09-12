### I. Remove one row - all row/Sort Icon Star Rating in Data Table:
**Reference :** [https://datatables.net/](https://datatables.net/)

**HTML**

```
<table class="table address-table table-hover" id="dataTable">
  <thead>
    <tr>
      <th width="42">
        <input id="allcb" class="cus-cb js-dropdown-target" type="checkbox" value="1">
        <label class="cus-cb-label" for="allcb"></label>
      </th>
      <th width="170">
        <a href="javascript:;">
            名前
            <span class="sort-icons">
                <i class="arrow-up-tb"></i>
            </span> 
        </a>
      </th>
      <th width="170">E mail アドレス</th>
      <th width="100">所属</th>
      <th width="275">
        <span class="set-group">
        グループ設定：
        <a class="sort-group" href="#">
          <span>全て</span>
          <i class="icon arrow-left-tb"></i>
        </a>
        </span>
      </th>
      <th class="plr0" width="24"></th>
      <th class="plr0" width="24">
        <a class="action-link action-favorite sort-favorite" href="#">
          <i class="icon ic-stars-title"></i>
        </a>
      </th>
      <th class="plr0" width="42">
        <a class="action-link action-delete" data-toggle="modal" data-target=".modal-user-all-delete" href="#">
          <i class="icon ic-delete"></i>
        </a>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td width="42">
        <input id="checkbox-row-2" class="cus-cb" type="checkbox" value="2">
        <label class="cus-cb-label" for="checkbox-row-2"></label>
      </td>
      <td><a class="name" href="#" data-toggle="modal" data-target=".modal-choose-name">1Hippo Taro</a></td>
      <td width="170"><span class="email">1hippo.la@hippotechusa.com</span></td>
      <td width="100"><span class="dept">総務部</span></td>
      <td width="275">
        <div class="dropdown dropdown-block">
          <button class="btn btn-dropdown" type="button" data-toggle="dropdown">
            <span class="label-setting">
              グループ設定 ： 
              <span class="slot-text">1. 総務部</span>
            </span>
            <span class="icon arrow-down-tb"></span>
          </button>
          <div class="dropdown-menu">
            <p class="label-set-level"><i class="icon icon-people"></i>グループ設定</p>
            <ul class="group-list">
              <li class="group-item">
                <a href="#">1：総務部</a>
              </li>
              <li class="group-item">
                <a href="#">2：人事部</a>
              </li>
              <li class="group-item">
                <a href="#">3：海外事業部</a>
              </li>
              <li class="group-item">
                <a href="#">4：営業部</a>
              </li>
            </ul>
          </div>
        </div>
      </td>
      <td class="plr0" width="24">
        <a class="action-link action-edit" href="#" data-toggle="modal" data-target=".modal-edit">
          <i class="icon ic-edits"></i>
        </a>
      </td>
      <td class="plr0" width="24">
        <a class="action-link action-favorite" href="javascript:void(0)">
          <i class="icon ic-rating"></i>
        </a>
      </td>
      <td class="plr0" width="42">
        <a class="action-link action-delete" data-toggle="modal" data-target=".modal-user-one-delete" href="#">
          <i class="icon ic-delete"></i>
        </a>
      </td>
    </tr>
    <tr>
      <td width="42">
        <input id="checkbox-row-3" class="cus-cb" type="checkbox" value="3">
        <label class="cus-cb-label" for="checkbox-row-3"></label>
      </td>
      <td><a class="name" href="#" data-toggle="modal" data-target=".modal-choose-name">2Hippo Taro</a></td>
      <td width="170"><span class="email">2hippo.la@hippotechusa.com</span></td>
      <td width="100"><span class="dept">総務部</span></td>
      <td width="275">
        <div class="dropdown dropdown-block">
          <button class="btn btn-dropdown" type="button" data-toggle="dropdown">
            <span class="label-setting">
              グループ設定 ： 
              <span class="slot-text">2. 人事部</span>
            </span>
            <span class="icon arrow-down-tb"></span>
          </button>
          <div class="dropdown-menu">
            <p class="label-set-level"><i class="icon icon-people"></i>グループ設定</p>
            <ul class="group-list">
              <li class="group-item">
                <a href="#">2：人事部</a>
              </li>
              <li class="group-item">
                <a href="#">3：海外事業部</a>
              </li>
              <li class="group-item">
                <a href="#">4：営業部</a>
              </li>
            </ul>
          </div>
        </div>
      </td>
      <td class="counter plr0" width="24">
        <a class="action-link action-edit" href="#" data-toggle="modal" data-target=".modal-edit">
          <i class="icon ic-edits"></i>
        </a>
      </td>
      <td class="counter plr0" width="24">
        <a class="action-link action-favorite" href="javascript:void(0)">
          <i class="icon ic-rating"></i>
        </a>
      </td>
      <td class="plr0" width="42">
        <a class="action-link action-delete" data-toggle="modal" data-target=".modal-user-one-delete" href="#">
          <i class="icon ic-delete"></i>
        </a>
      </td>
    </tr>
    <tr>
      <td width="42">
        <input id="checkbox-row-4" class="cus-cb" type="checkbox" value="4">
        <label class="cus-cb-label" for="checkbox-row-4"></label>
      </td>
      <td><a class="name" href="#" data-toggle="modal" data-target=".modal-choose-name">3Hippo Taro</a></td>
      <td width="170"><span class="email">3hippo.la@hippotechusa.com</span></td>
      <td width="100"><span class="dept">総務部</span></td>
      <td width="275">
        <div class="dropdown dropdown-block">
          <button class="btn btn-dropdown" type="button" data-toggle="dropdown">
            <span class="label-setting">
              グループ設定 ： 
              <span class="slot-text">2. 人事部</span>
            </span>
            <span class="icon arrow-down-tb"></span>
          </button>
          <div class="dropdown-menu">
            <p class="label-set-level"><i class="icon icon-people"></i>グループ設定</p>
            <ul class="group-list">
              <li class="group-item">
                <a href="#">2：人事部</a>
              </li>
              <li class="group-item">
                <a href="#">3：海外事業部</a>
              </li>
              <li class="group-item">
                <a href="#">4：営業部</a>
              </li>
            </ul>
          </div>
        </div>
      </td>
      <td class="counter plr0" width="24">
        <a class="action-link action-edit" href="#" data-toggle="modal" data-target=".modal-edit">
          <i class="icon ic-edits"></i>
        </a>
      </td>
      <td class="counter plr0" width="24">
        <a class="action-link action-favorite" href="javascript:void(0)">
          <i class="icon ic-rating"></i>
        </a>
      </td>
      <td class="plr0" width="42">
        <a class="action-link action-delete" data-toggle="modal" data-target=".modal-user-one-delete" href="#">
          <i class="icon ic-delete"></i>
        </a>
      </td>
    </tr>
    <tr>
      <td width="42">
        <input id="checkbox-row-5" class="cus-cb" type="checkbox" value="5">
        <label class="cus-cb-label" for="checkbox-row-5"></label>
      </td>
      <td><a class="name" href="#" data-toggle="modal" data-target=".modal-choose-name">4Hippo Taro</a></td>
      <td width="170"><span class="email">4hippo.la@hippotechusa.com</span></td>
      <td width="100"><span class="dept">総務部</span></td>
      <td width="275">
        <div class="dropdown dropdown-block">
          <button class="btn btn-dropdown" type="button" data-toggle="dropdown">
            <span class="label-setting">
              グループ設定 ： 
              <span class="slot-text">2. 人事部</span>
            </span>
            <span class="icon arrow-down-tb"></span>
          </button>
          <div class="dropdown-menu">
            <p class="label-set-level"><i class="icon icon-people"></i>グループ設定</p>
            <ul class="group-list">
              <li class="group-item">
                <a href="#">2：人事部</a>
              </li>
              <li class="group-item">
                <a href="#">3：海外事業部</a>
              </li>
              <li class="group-item">
                <a href="#">4：営業部</a>
              </li>
            </ul>
          </div>
        </div>
      </td>
      <td class="counter plr0" width="24">
        <a class="action-link action-edit" href="#" data-toggle="modal" data-target=".modal-edit">
          <i class="icon ic-edits"></i>
        </a>
      </td>
      <td class="counter plr0" width="24">
        <a class="action-link action-favorite" href="javascript:void(0)">
          <i class="icon ic-rating"></i>
        </a>
      </td>
      <td class="plr0" width="42">
        <a class="action-link action-delete" data-toggle="modal" data-target=".modal-user-one-delete" href="#">
          <i class="icon ic-delete"></i>
        </a>
      </td>
    </tr>
    <tr>
      <td width="42">
        <input id="checkbox-row-6" class="cus-cb" type="checkbox" value="6">
        <label class="cus-cb-label" for="checkbox-row-6"></label>
      </td>
      <td><a class="name" href="#" data-toggle="modal" data-target=".modal-choose-name">5Hippo Taro</a></td>
      <td width="170"><span class="email">5hippo.la@hippotechusa.com</span></td>
      <td width="100"><span class="dept">総務部</span></td>
      <td width="275">
        <div class="dropdown dropdown-block">
          <button class="btn btn-dropdown" type="button" data-toggle="dropdown">
            <span class="label-setting">
              グループ設定 ： 
              <span class="slot-text">2. 人事部</span>
            </span>
            <span class="icon arrow-down-tb"></span>
          </button>
          <div class="dropdown-menu">
            <p class="label-set-level"><i class="icon icon-people"></i>グループ設定</p>
            <ul class="group-list">
              <li class="group-item">
                <a href="#">2：人事部</a>
              </li>
              <li class="group-item">
                <a href="#">3：海外事業部</a>
              </li>
              <li class="group-item">
                <a href="#">4：営業部</a>
              </li>
            </ul>
          </div>
        </div>
      </td>
      <td class="counter plr0" width="24">
        <a class="action-link action-edit" href="#" data-toggle="modal" data-target=".modal-edit">
          <i class="icon ic-edits"></i>
        </a>
      </td>
      <td class="counter plr0" width="24">
        <a class="action-link action-favorite" href="javascript:void(0)">
          <i class="icon ic-rating"></i>
        </a>
      </td>
      <td class="plr0" width="42">
        <a class="action-link action-delete" data-toggle="modal" data-target=".modal-user-one-delete" href="#">
          <i class="icon ic-delete"></i>
        </a>
      </td>
    </tr>
  </tbody>
</table>
```

**JS**

``` javascript
var tableAddress = $('#dataTable').DataTable({
  "bPaginate": false,
  "bLengthChange": false,
  "bFilter": false,
  "bInfo": false,
  "bSort": true,
  "bProcessing": true,
  "columnDefs": [{
    targets: [6],
    render: function(data, type, full, meta) {
      if (type == 'sort') {
        var val = $(data).find('.ic-rating').hasClass('selected') ? 0 : 1;
        return val;
      } else {
        return data;
      }
    }
  }]
});

$('#dataTable tbody').on('click', 'tr', function() {
  if ($(this).hasClass('selected')) {
    $(this).removeClass('selected');
  } else {
    tableAddress.$('tr.selected').removeClass('selected');
    $(this).addClass('selected');
  }
});
$('.address-table tbody tr').each(function() {
  //Rating
  $(this).parent().parent().find('thead').on('click', '.ic-stars-title', function(e) {
    $(this).toggleClass('selected');
  });
  var isClicked = false;
  $(this).on('click', '.ic-rating', function() {
    isClicked = true;
    $(this).addClass('selected');
  });
  $(this).on('click', '.ic-rating.selected', function() {
    if (isClicked) {
      $(this).removeClass('selected');
    }
  });

  // Add hightlight row table
  $(this).parent().find('.action-edit').click(function() {
    $(this).parent().parent().addClass('row-checked');
  });
  $(this).parent().find('.action-delete').click(function() {
    $(this).parent().parent().addClass('row-checked');
  });
  $(this).parent().find('.name').click(function() {
    $(this).parent().parent().addClass('row-checked');
  });
});

// Unhightlight row table
$('.modal-edit,.modal-info-user,.modal-user-one-delete,.modal-user-all-delete,.modal-choose-name').on('hidden.bs.modal', function(event) {
  $('.address-table tbody tr').removeClass('row-checked');
});
// re-draw table when click sort favorite
$('.sort-favorite').click(function(e) {
  e.preventDefault();
  tableAddress.rows().invalidate().draw();
});
// =============================================================================
// Handle event checked all
// =============================================================================
$('#allcb').change(function() {
  if ($(this).prop('checked')) {
    $('.address-table tbody tr td:first-child input[type="checkbox"]').each(function() {
      $(this).prop('checked', true);
    });
  } else {
    $('.address-table tbody tr td:first-child input[type="checkbox"]').each(function() {
      $(this).prop('checked', false);
    });
  }
});

// =============================================================================
// Handle event remove all row table
// =============================================================================
$('.address-table > thead > tr > th').on('click', '.action-delete', function() {
  var _this = $(this).parent().parent().parent().parent().find('tbody');
  $('.btn-remove-row').on('click', function() {
    $(".modal-user-all-delete").modal("hide");
    tableAddress.rows().remove().draw();
  });
});
// =============================================================================
// Handle event remove one row table
// =============================================================================
$('.address-table tbody tr td').on('click', '.action-delete', function() {
  var _this = $(this).parent().parent();
  $('.btn-remove-row').on('click', function(e) {
    e.preventDefault();
    $(".modal-user-one-delete").modal("hide");
    tableAddress.row('.selected').remove().draw(false);
  });
});

```