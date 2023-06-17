# Algorithm

"Thuật toán hình chữ nhật tối đại" (Maximal Rectangle Algorithm) : Thuật toán này áp dụng cơ chế quy hoạch động để tìm kiếm hình chữ nhật lớn nhất.
- Ý tưởng chính của thuật toán là xem mỗi hàng trong ma trận như một đường đơn giản và áp dụng thuật toán:
1. Sử dụng "[Largest Rectangle in Histogram](https://github.com/DcViet/Algorithm/blob/main/assets/Largest_Histogram.md)" trên các hàng để tìm kiếm hình chữ nhật lớn nhất.
2. Tính toán chiều rộng và chiều cao của các hình chữ nhật con: duyệt qua từng hàng của ma trận và tính toán chiều rộng của hình chữ nhật tối đại kết thúc tại mỗi cột. Sau đó, ta tính toán diện tích của hình chữ nhật tối đại dựa trên chiều rộng và chiều cao đã tính toán.
