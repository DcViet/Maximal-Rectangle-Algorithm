Thuật toán *"Largest Rectangle in Histogram"* được sử dụng để tìm hình chữ nhật lớn nhất trong một `histogram`. 

- Histogram là một biểu đồ cột mà mỗi cột đại diện cho một giá trị trong mảng. Ý tưởng chính của thuật toán là tìm ra cột có chiều cao nhỏ nhất trong các cột liên tiếp và tính diện tích lớn nhất có thể tạo ra từ cột đó.
- Thuật toán "Largest Rectangle in Histogram" có thể được triển khai bằng cách sử dụng một [stack](https://github.com/DcViet/Algorithm/blob/main/assets/stack.md) để lưu trữ các chỉ số của các cột trong histogram. Ý tưởng là duyệt qua từng cột và thực hiện các bước sau:
1. Nếu stack rỗng hoặc chiều cao của cột hiện tại lớn hơn chiều cao của cột trên đỉnh stack, đẩy chỉ số của cột hiện tại vào stack.
2. Nếu chiều cao của cột hiện tại nhỏ hơn chiều cao của cột trên đỉnh stack, lấy chiều cao của cột trên đỉnh stack và tính diện tích của hình chữ nhật có chiều cao đó. Diện tích này là chiều cao nhân với khoảng cách từ chỉ số hiện tại đến chỉ số của cột trên đỉnh stack.
3. Lặp lại bước 2 cho đến khi stack rỗng hoặc chiều cao của cột hiện tại lớn hơn chiều cao của cột trên đỉnh stack.
4. Sau khi duyệt qua tất cả các cột, kiểm tra xem stack còn phần tử nào hay không. Nếu còn, lấy chiều cao của cột trên đỉnh stack và tính diện tích của hình chữ nhật có chiều cao đó với chiều rộng là khoảng cách từ chỉ số của cột trên đỉnh stack đến cuối danh sách cột.
5. So sánh và cập nhật diện tích lớn nhất đã tìm thấy với diện tích hiện tại.
6. Trả về diện tích lớn nhất.
