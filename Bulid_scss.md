I. Biên dịch SCSS:
1. Gulp
2. Grunt
3. runtime
4. complie:

- Tiếp theo bạn cài đặt Sass bằng cách mở CMD và gõ:

  ```gem install sass```

- Sass cung cấp hai định dạng tập tin mở rộng .scss và .sass. Để chuyển đổi tập tin sass sang .css bạn thực hiện lệnh sau:

  ```sass stylesheet.scss stylesheet.css```

  ```sass --watch scss/common.scss:css/common.css```

  ```sass --watch styles/index.scss:html/app/css/index.css```

- Để thực hiện chuyển đổi .scss và .css trong quá trình làm việc bạn thực hiện lệnh sau:

  ```sass --watch stylesheet.scss:stylesheet.css```

- Bạn làm việc với thư mục và cần chuyển đổi tất cả thì có thể thực hiện lệnh sau:

  ```sass --watch sass:css```