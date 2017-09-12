### Cốt lõi nhất của các đơn vị là front size body luôn có giá trị là 16px. Từ giá trị này mà người làm web có thể qui về giá trị font-size ở mỗi element trong bản Design.

Tham Khảo : https://www.sitepoint.com/understanding-and-using-rem-units-in-css/

#### I. Unit %:

  ```body {
    font-size:87.5%; /* Tương đương 14px */

    /* font-size:75%; Tương đương 12px */
  }```

  - Chẳng hạn như font-size thẻ h1 đo trong PSD là 16px thì lấy ```16:14=1.1429```, lấy ```1.1429X100%= 114.29%```, con số ```114.29%``` sẽ là font-size của h1.

#### II. Unit EM:
   
  - em : Relative to the font-size of the element (2em means 2 times the size of the current font)

  - Trường hợp body ```{ font-size:62.5%; }```

  - ```body { font-size:62.5%; }  /* =10px */```

  - ```h1{ font-size: 2.4em; } /* =24px */```

  - ```p{ font-size: 1.4em; } /* =14px */```

  - ```li{ font-size: 1.4em; } /* =14px? */```

- Nếu  body có  ```font-size:62.5%;```  thì tương đương với 10px; , Như vậy  nếu muốn tính đơn vị em thì  cứ lấy đơn vị ```px``` chia 10.

#### III. Unit REM:

  -Trường hợp : Với các đơn vị rem, điều này là một đơn giản:
  
  - Rem : Relative to font-size of the root element

  ```html {
    font-size: 100%; tương đương với 16px
  }
  ul {
    font-size: 0.75rem;
  }```

  - Nếu ul có font-size: 12px muốn đổi sang đơn vị rem thì lấy 12:16= 0.75.

  - Quy đổi các đơn vị: bằng cách lấy đơn vị px chia cho 16 sẽ ra đơn vị rem.

  ```10px = 0.625rem

     12px = 0.75rem

     14px = 0.875rem

     16px = 1rem (cơ sở)

     18px = 1.125rem

     20px = 1.25rem

     24px = 1.5rem

     30px = 1.875rem

     32px = 2rem```

  - Trường hợp body { font-size:62.5%; }

  ```body { font-size:62.5%; }  /* =10px */
  h1{ font-size: 2.4em; } /* =24px */
  p{ font-size: 1.4em; } /* =14px */
  li{ font-size: 1.4em; } /* =14px? */```

  - Cách sử dụng font-size ở các trình duyệt ko hỗ trợ đơn vị rem:
  ```html {
    font-size: 62.5%;
  }
  body {
    font-size: 14px;
    font-size: 1.4rem;
  }
  h1 {
    font-size: 24px;
    font-size: 2.4rem;
  }
```