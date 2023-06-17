# Maximal Rectangle Algorithm 

"Thuật toán hình chữ nhật tối đại" (Maximal Rectangle Algorithm) : Thuật toán này áp dụng cơ chế quy hoạch động để tìm kiếm hình chữ nhật lớn nhất.
- Ý tưởng chính của thuật toán là xem mỗi hàng trong ma trận như một đường đơn giản và áp dụng thuật toán:
##
1. Sử dụng "[Largest Rectangle in Histogram](https://github.com/DcViet/Algorithm/blob/main/assets/Largest_Histogram.md)" trên các hàng để tìm kiếm hình chữ nhật lớn nhất.
```
def maximal_rectangle(matrix):
    if not matrix:
        return 0

    m = len(matrix[0])
    heights = [0] * (m + 1)
    max_area = 0

    for row in matrix:
        for j in range(m):
            if row[j] == '1':
                heights[j] += 1
            else:
                heights[j] = 0

        stack = [-1]
        for j in range(m + 1):
            while heights[j] < heights[stack[-1]]:
                h = heights[stack.pop()]
                w = j - 1 - stack[-1]
                max_area = max(max_area, h * w)
            stack.append(j)

    return max_area

# Ma trận mẫu
matrix = [
    '100000000',
    '111111110',
    '001111100',
    '001111100',
    '000000000',
]

area = maximal_rectangle(matrix)
print("Maximal Rectangle Area:", area)
```
> Ánh xạ kiến thức:
> 1. Đầu tiên, kiểm tra xem ma trận có rỗng không. Nếu là ma trận rỗng, trả về diện tích hình chữ nhật tối đại là 0.
> 2. Khởi tạo biến m để lưu số cột của ma trận và một mảng heights với kích thước là m + 1. Mảng heights sẽ lưu trữ chiều cao của các cột.
> 3. Tiếp theo, lặp qua từng hàng trong ma trận. Với mỗi hàng, duyệt qua từng cột.
> 4. Nếu ký tự trong ma trận tại hàng và cột tương ứng là "1", tăng giá trị chiều cao của cột đó trong mảng heights lên 1. Nếu không, đặt chiều cao của cột đó trong mảng heights về 0.
> 5. Sau khi duyệt qua tất cả các cột trong hàng hiện tại, thực hiện thuật toán "Largest Rectangle in Histogram" trên mảng heights. Đoạn mã sử dụng một stack để tìm kiếm hình chữ nhật lớn nhất trong mảng heights. Khi tìm thấy một cột có chiều cao nhỏ hơn cột trên đỉnh stack, ta lấy cột trên đỉnh stack ra khỏi stack và tính diện tích của hình chữ nhật được tạo bởi cột đó. Diện tích này được so sánh và cập nhật với diện tích lớn nhất đã tìm thấy.
> 6. Lặp lại quá trình trên cho tất cả các hàng trong ma trận.
> 7. Trả về diện tích lớn nhất tìm được.
##
2. Tính toán chiều rộng và chiều cao của các hình chữ nhật con: duyệt qua từng hàng của ma trận và tính toán chiều rộng của hình chữ nhật tối đại kết thúc tại mỗi cột. Sau đó, ta tính toán diện tích của hình chữ nhật tối đại dựa trên chiều rộng và chiều cao đã tính toán.

```
def maximal_rectangle(matrix):
    if not matrix:
        return 0

    max_area = 0
    m = len(matrix[0])
    heights = [0] * m

    for row in matrix:
        for j in range(m):
            if row[j] == '1':
                heights[j] += 1
            else:
                heights[j] = 0

        area = calculate_area(heights)
        max_area = max(max_area, area)

    return max_area

def calculate_area(heights):
    n = len(heights)
    left = [0] * n
    right = [n] * n
    stack = []

    for i in range(n):
        while stack and heights[stack[-1]] >= heights[i]:
            stack.pop()

        if stack:
            left[i] = stack[-1] + 1

        stack.append(i)

    stack = []

    for i in range(n - 1, -1, -1):
        while stack and heights[stack[-1]] >= heights[i]:
            stack.pop()

        if stack:
            right[i] = stack[-1]

        stack.append(i)

    max_area = 0

    for i in range(n):
        area = (right[i] - left[i]) * heights[i]
        max_area = max(max_area, area)

    return max_area

# Ma trận mẫu
matrix = [
    '100000000',
    '111111110',
    '001111100',
    '001111100',
    '000000000',
]

area = maximal_rectangle(matrix)
print("Maximal Rectangle Area:", area)
```
> Bước 1: Tính toán chiều cao của từng cột trong ma trận.
> - Khởi tạo một mảng có cùng kích thước với số cột trong ma trận, ban đầu tất cả các phần tử đều bằng 0.
> - Duyệt qua từng hàng của ma trận.
> - Với mỗi phần tử ở hàng hiện tại và cột tương ứng, nếu nó là '1', tăng giá trị của phần tử tại cột đó trong mảng chiều cao lên 1. Nếu nó là '0', đặt giá trị của phần tử tại cột đó trong mảng chiều cao về 0.

> Bước 2: Xác định hình chữ nhật tối đại.
> - Duyệt qua từng hàng của ma trận.
> - Đối với hàng hiện tại, sử dụng mảng chiều cao đã tính ở Bước 1 để xác định chiều cao của hình chữ nhật tối đại mà có hàng hiện tại là hàng đáy.
> - Với mỗi phần tử trong hàng hiện tại, ta xem nó như là đỉnh của một hình chữ nhật có chiều cao tương ứng trong mảng chiều cao.
> - Với mỗi đỉnh, ta tính toán chiều rộng của hình chữ nhật bằng cách duyệt sang trái và sang phải từ đỉnh đó, đến khi gặp một chiều cao nhỏ hơn đỉnh hoặc đến cột đầu tiên hoặc cột cuối cùng.
> - Với mỗi hình chữ nhật được tính toán, ta so sánh diện tích với diện tích tối đa hiện tại và cập nhật nếu diện tích mới tìm được lớn hơn.

## Bài toán chứa nhiều ký tự khác nhau

<img src="https://scontent.fsgn5-2.fna.fbcdn.net/v/t39.30808-6/354064454_954295605691094_3765286956672078844_n.jpg?_nc_cat=105&ccb=1-7&_nc_sid=5cd70e&_nc_ohc=8HIzEoPP3jcAX8LnkK0&_nc_ht=scontent.fsgn5-2.fna&oh=00_AfDs9CxytbAWyvHv_kPlCkOdW9qTAmTvUrVDMTFjbubyjw&oe=6491B980" alt="vidu" width="60%" />

## 
<img src="https://cdn.programiz.com/sites/tutorial2program/files/pc_logo.svg" att="programiz" width= "25%" />

{@gist: Gist ID or URL}
[RUN](https://www.programiz.com/python-programming/online-compiler/) 
> kết quả:
```
ccccccc
ccccccc
ccccccc
ccccccc
ccccccc
```

