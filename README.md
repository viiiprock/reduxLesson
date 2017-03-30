# Học REACT REDUX 

## Cài đặt

Nếu bạn sử dụng trên máy thì có thể sử dụng create-react-app hoặc bất kỳ react boilerplate nào bạn thích (tốt nhất là sử dụng webpack).
Bạn có thể kiểm tra dependencies đã có hay chưa.

Với bài viết này, tôi sử dụng [JS Bin](http://jsbin.com/) nên có hơi khác một chút so với 

* redux
* react-redux

## Chuẩn bị kiến thức

Đương nhiên là bạn cần biết qua React và JavaScript

## Giới thiệu 

Tôi viết bài này vì tôi là một tay ngang về lập trình, viết bài giúp tôi học tốt hơn nên đây chưa hẳn là lòng tốt mà viết bài cho các bạn đọc, tôi viêt cho tôi tự sướng cái đã.

Người ta luôn nói Redux cực kỳ dễ nhưng thực tế thì tôi đã học rất nhiều phen rồi mà nó cứ loạn hết cả lên, làm sao có thể nuốt nổi mấy cái khái niệm lạ lùng của Redux. Do đó, tôi cố gắng viết bài này một cách chậm rãi, tường tận nhất, diễn giải một cách dễ hiểu nhất cho ai mới bắt đầu học Redux. Có thể nói huỵch toẹt là Redux for dummies 


## Nội dung

### Quy trình của Redux

Ok, cái này đầy rẫy trên mạng, tôi chỉ note ngắn gọn vài điểm chính thôi.

* TL,DR: Nhắc lại một chút, bạn đã làm quen với phương thức quản lý props, state của React với chu trình LifeCycle của nó như 
1. Mounting state bằng `constructor()`, `componentWillMount()`, `render()`,`componentDidMount()`, 
2. Update bằng `componentWillReceiveProps()`, `shouldComponentUpdate()`,`componentWillUpdate()`, `render()`, `componentDidUpdate()`
3. Destroy bằng `componentWillUnmount()`

Tại sao lại nhiều quy trình vậy?! thực sự tôi chưa có điều kiện để dùng hết một đống chu trình như ở trên, tuy nhiên với cách quản lý như vậy thì khi viết một ứng dụng nó có nhiều thao tác giống nhau, hoặc hơi giống nhau, bạn sẽ nhận ra rằng mình đang gặp rắc rối về quản lý state như thế nào. Vì vậy, không phải lúc nào cũng dùng React hoặc nhất thiết phải dùng Redux để quản lý state, cái đó phụ thuộc vào cái bạn đang làm, nhưng tốt nhất nên biết cả hai (một số bạn có thể tìm hiểu và sử dụng MobX thay cho Redux, ok, đường nào cũng tới Paris).



