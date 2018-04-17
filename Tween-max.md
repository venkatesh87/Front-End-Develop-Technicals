## TweenMax

1. [TweenMax](https://greensock.com/docs/TweenMax/static.selector)

>**Note Parameters**
- ```autoAlpha```: 0 tương đương với opacity: 0
- ```xPercent, yPercent```: Theo thông số CSS, tỷ lệ phần trăm biến đổi luôn luôn liên quan đến phần tử, chứ không phải là cha mẹ nó.
- ```delay```: Number - Số lần chậm trễ trong giây (hoặc khung cho khung dựa trên tweens) trước khi bắt đầu animation.
- ```paused```: Boolean - Nếu ```true```, animation sẽ tạm dừng ngay lập tức ngay khi tạo ra.
- ```onComplete()```: Function - Một chức năng cần được gọi khi hoàn thành hoạt hình.
- ```onCompleteScope```: Object - Xác định phạm vi của các chức năng onComplete (cái gì "này" dùng để chỉ bên trong hàm đó).
- ```useFrames```:  Boolean - Nếu khung điều khiển là đúng, thời gian của các đối tượng sẽ dựa trên khung thay vì giây vì nó được thêm vào khung gốc dựa trên khung gốc. Điều này gây ra cả thời gian và sự chậm trễ của nó dựa trên khung. Chế độ thời gian hoạt ảnh của hình ảnh động luôn được xác định bởi dòng thời gian gốc của hình ảnh.
- ```tweens```:  Array - To ngay lập tức chèn một vài tween vào timeline, sử dụng đặc tính tweens đặc biệt để vượt qua trong một mảng của TweenLite / TweenMax / TimelineLite / TimelineMax trường hợp. Bạn có thể sử dụng kết hợp với các thuộc tính đặc biệt và sắp xếp để thiết lập trình tự phức tạp với mã tối thiểu. Các giá trị này chỉ đơn giản được truyền vào phương thức add ().
- ```stagger```:  Number - Chỉ được sử dụng kết hợp với đặc tính đặc biệt của tweens khi nhiều tweens được chèn vào ngay lập tức. Nó staggers tweens của một số lượng thời gian trong vài giây (hoặc trong khung nếu useFrames là đúng). Ví dụ, nếu giá trị stagger là 0.5 và thuộc tính "align" được thiết lập là "start", thì tween thứ hai sẽ bắt đầu 0,5 giây sau khi bắt đầu đầu tiên, sau đó 0,5 giây sau đó phần thứ ba sẽ bắt đầu, v.v. Nếu thuộc tính align là "sequence", sẽ có thêm 0.5 giây giữa mỗi Tween. Giá trị này đơn giản được truyền vào phương thức add (). Mặc định là 0.
- ```align```: String - Chỉ sử dụng kết hợp với thuộc tính đặc biệt của tweens khi nhiều tweens được chèn vào ngay lập tức. Giá trị đơn giản được truyền vào phương thức add (). Mặc định là "bình thường". Các tùy chọn là:
  + "sequence": sắp xếp các tween một-sau-nhau trong một chuỗi 
  + "start": sắp xếp thời gian bắt đầu của tất cả các tweens (bỏ qua sự chậm trễ) 
  + "normal": căn chỉnh thời gian bắt đầu của tất cả các tweens (tôn vinh sự chậm trễ)
- ```onStart()```: Một chức năng nên được gọi khi bắt đầu animation (khi thời gian thay đổi từ 0 sang một số giá trị khác có thể xảy ra nhiều lần nếu tween được khởi động lại nhiều lần).
- ```onStartScope```: Object - Xác định phạm vi của chức năng onStart ("cái này" dùng để chỉ bên trong hàm đó).
- ```onUpdate```(): Một chức năng cần được gọi mỗi khi cập nhật animation (trên mỗi khung khi hoạt ảnh hoạt động).
- ```onUpdateScope```: Object - Xác định phạm vi của chức năng onUpdate (cái "cái này" đề cập đến bên trong hàm đó).
- ```onRepeat```: Function - Một chức năng cần được gọi mỗi lần animation lặp lại.
- ```onRepeatScope```: Object - Xác định phạm vi của chức năng onRepeat (cái này "cái này" đề cập đến bên trong hàm đó).
- ```onReverseComplete```:  Function - Một chức năng cần được gọi khi animation đã bắt đầu lại từ hướng ngược lại.. Ví dụ, nếu ```reverse()``` được gọi là tween sẽ di chuyển về phía đầu của nó và khi thời gian của nó đạt đến 0, onReverseComplete sẽ được gọi. Điều này cũng có thể xảy ra nếu các hình ảnh động được đặt trong một TimelineLite hoặc trường hợp TimelineMax được đảo ngược và đóng các hoạt hình ngược trở lại (hoặc quá khứ) đầu.
- 

