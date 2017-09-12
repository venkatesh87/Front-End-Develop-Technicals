## Image dù lớn hay nhỏ đều nằm trong khung hình 

- Được canh giữa left và right với khung chứa nó.
- Được canh đều top và bottom với khung chứa nó.
- Tất cả tag &lt;img&gt; đều được bọc bởi tag &lt;p&gt;.
- Canh giũa và fix theo độ cao tối đa của image trong cms8341 để tránh vở hình.
+ Case 1

```
.image{
    margin: 0 auto;
    display: block;
    width: auto !important;
    max-height: 250px;
}

```
+ Case 2

```
<p class="img"><img alt="" width="178" height="110" src=""></p>
```
```
#tmp_contents .bunkazai .juyo .juyo_cnt .img {
    float: left;
    margin: 0 20px 0 0;
    width: 180px;
}
```
```
#tmp_contents .bunkazai .juyo .juyo_cnt .img img {
    height: auto;
    max-width: 100%;
}
```

+ Case 3

```
<div class="box_event_img">
<p><img src="/things/events/images/genjimatsuri_1.jpg" alt="" width="246" height="368"></p>
</div>
```

```
#tmp_slide_event .box_event_img p {
    width: 308px;
    height: 232px;
    overflow: hidden;
}
```

```
#tmp_slide_event .box_event_img img {
    position: relative;
    top: 50%;
    left: 50%;
    max-height: 232px\9;
    width: auto;
    height: 100%;
    -webkit-transform: translate(-50%,-50%);
    -ms-transform: translate(-50%,-50%);
    transform: translate(-50%,-50%);
}
```