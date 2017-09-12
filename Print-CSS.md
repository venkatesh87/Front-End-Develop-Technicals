# Check List Front End CMS8341
## Print CSS

/cms8341/shared/templates/free/style/edit.css
 
 /* ==================================================
 print
 ================================================== */

Master guideline.2016

page 19 : Setting in ấn

### Top page

* Không tiến hành xử lý như xóa chẳng hạn

※Sẽ chỉnh sửa những lỗi hư hỏng bị xóa dođiều chỉnh độ rộng của dòng và hình ảnh, nhưng không thể đối ứng giống hoàntoàn với màn hình.

* Xem xét đối ứng nếu có nguyện vọng khác

### Page terminal

1. Xóa vùng hoặc element bên dưới
    - Không phải là logo của #tmp_header
    - Navigation ( chẳng hạn như #tmp_gnavi・#tmp_lnavi）
    - Plugin, page navy ( back về đầu page,… ),button SNS
    - Không phải logo , copy right, address của#tmp_footer
    - feedback
    - background(color, image)
2. Set độ rộng vùng body text thành 100%
    - Vẫn cố định site độ rộng cố định để duy trì design.

3. Khi trang trí thì chỉ giữ lại cái liên quan đến element của body text.

   - Ngoài element bên trong body text , màu background, image background, line thì sẽ xóa.

Màu background, image background, line của element trong body text chẳng hạn như tiêu đề-list icon-parts khác thì sẽ giữ lại.

 4. Hiển thị đường ngăn cách với body text

    - border-bottom của #tmp_header

    - border-top của #tmp_footer

5. Confirm hiển thị bằng print monochrome

   - Điều chỉnh việc xóa background những điểm khó đọc chẳng hạn. 

   ![Picture](http://pub.demo.products26.cms8341.jp/lecture/images/cap.png)

