## Accessibility

### CMS8341
#### - Font-Size : Tăng kích thước fon-size(Lớn, nhỏ, bình thường)
#### - Color Contrast : Tương phản màu
#### - Read the text software & Ruby. (Cài phần mềm để có thể đọc được text)

### Link Tham khảo : https://www.w3.org/TR/WCAG20/

- Phát triển cho người khiếm thị, khiếm thính, khuyết tật và thân thiện cho người dùng bình thường. 
- Content của page có nghe được âm thanh.
- Có 4 điểm chú ý :

#### Point 1 :

   - Mắt (Khiếm Thị)
   - Tai (Khiếm thính)

#### Point 2 : 

   - Dễ thao tác phím keyboard tab.

#### Point 3 :

  - Người chậm chạp

#### Point 4 : Robust 

##### - Source Code phải chính xác.

      + Đối ứng người khiếm thị, khiếm thính những content ko phải là text để đầy đủ thông tin.
      + Img có thuộc tính alt.
      + Iframe có thuộc tính title.

##### 1. Perceivable : 

   - Chú ý đến contrast, contrast thì liên quan đến Design set tỉ lệ 4.5 : 1 contrast.
   - Tool : Colour Contrast Analyser. Tuy nhiên còn chú ý liên quan đến css . Xem thuộc tính color & background.

##### 2. Operable : 

   - Làm sao đó để sử dụng tất cả các chức năng từ keyboard dùng thao tác tab.
   - Trình tự sort và bề ngoài map với nhau.
   - user có đủ thời gian để đọc dc content.
   - Những cái nào trên 4s thì phải có nút điều khiển Start/Stop.
   - Liên quan đến Animation cũng trên 4s.
   - Breakcrum :
   - Focus order : Focus theo trình tự trên toàn page.

##### 3. Language của page :

   - Nếu là tiếng Anh thì set ngôn ngữ cho nó.
   - Nếu page toàn tiếng Nhật thì set ở trong html có language là tiếng Nhật.
   - Nếu có một số ít tiếng Anh or tiếng Nhật thì set riêng cho nó.
   - Có bao nhiêu ngôn ngữ khác nhau thì đều set hết.
   - Phải chuẩn bị data đầy đủ sau này áp dụng.

   - H57： Sử dụng thuộc tính ngôn ngữ của element html（Rank đạt đượcA/達成等級A）
   - http://waic.jp/docs/WCAG-TECHS/H57.html

     1.Chỉ định thuộc tính lang và ( hoặc) xml:lang vào element html.

     2.Trường hợp sử dụng ngôn ngữ khác với thuộc tính lang mà chỉ định bằng element html trong content thì sẽ tiến hành markup bằng thuộc tính lang.

   - Ví dụ：

     &lt;a lang="en" xml:lang="en" href="/cms8341/foreign/english.html"&gt;
        &lt;img alt="English" width="48" height="31" src="/shared/images/header/hnavi_english.gif"&gt;
     &lt;/a&gt;

   - Trường hợp là XHTML, thì sẽ viết sát vào nhau   lang="en" xml:lang="en".

     ※Về Copyright thì cũng tương tự 

     &lt;p id="tmp_copyright" lang="en" xml:lang="en"&gt;Copyright &copy; Glode City. All Rights Reserved.&lt;/p&gt;

##### 4. Form

   - H44： Sử dụng element label, gán liên quan label của text với form・control (Rank đạt được A)

   - http://waic.jp/docs/WCAG-TECHS/H44.html

   - H65： Khi không thể sử dụng element label thì sẽ sử dụng element title rồi đặc định form・control (Rank đạt được A)

   - http://waic.jp/docs/WCAG-TECHS/H65.html

   - Ex1（H44）

       &lt;label for="firstname">お名前:&lt;/label&gt; 

       &lt;input type="text" name="firstname" id="firstname" /&gt;

   - Ex 2（H65）

       &lt;select title="検索対象" id="scope"&gt;
          …
       &lt;/select&gt; 

##### 5. Validator dùng của w3c : https://validator.w3.org/#validate_by_input

### Checklist Accesibility Standard

  http://accessibility.voxmedia.com/#designers

  https://ebay.gitbooks.io/mindpatterns/content/messaging/inlinenotice.html

  http://ianmcburnie.github.io/mindpatterns/accordion/

  https://medium.com/salesforce-ux/7-things-every-designer-needs-to-know-about-accessibility-64f105f0881b#.cn3f15fgp
  
##### 6. Checklist Accessibility with HTML5.

  **Refer:** https://a11yproject.com/checklist
  

