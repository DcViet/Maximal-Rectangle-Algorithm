**Stack** là một cấu trúc dữ liệu cơ bản trong lập trình, được sử dụng để lưu trữ dữ liệu theo nguyên tắc "Last-In-First-Out" (LIFO)
## Ví dụ 
- Trong thuật toán tìm kiếm đường đi (DFS) trên đồ thị, stack được sử dụng để lưu trữ các đỉnh và duyệt qua các đỉnh liền kề theo nguyên tắc LIFO.
```
# ví dụ về tìm kiếm đường đi (DFS) trên đồ thị bằng cách sử dụng stack
def dfs(graph, start):
    visited = set()
    stack = [start]
    
    while stack:
        vertex = stack.pop()
        
        if vertex not in visited:
            visited.add(vertex)
            print(vertex)
            
            # Lặp qua tất cả các đỉnh kề của đỉnh hiện tại
            for neighbor in graph[vertex]:
                if neighbor not in visited:
                    stack.append(neighbor)

# Đồ thị mẫu
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}

# Gọi hàm DFS
dfs(graph, 'A')

```
> Trong đoạn mã trên, chúng ta sử dụng một stack để lưu trữ các đỉnh cần duyệt. Ban đầu, ta đẩy đỉnh bắt đầu (trong ví dụ là 'A') vào stack. Sau đó, chúng ta thực hiện vòng lặp while cho đến khi stack rỗng. Trong vòng lặp, ta lấy đỉnh trên đỉnh của stack, kiểm tra xem nó đã được ghé thăm hay chưa. Nếu chưa, ta đánh dấu đỉnh đó là đã ghé thăm và in ra giá trị của đỉnh đó. Tiếp theo, ta duyệt qua tất cả các đỉnh kề của đỉnh hiện tại và đẩy các đỉnh chưa được ghé thăm vào stack. Quá trình này tiếp tục cho đến khi ta đã duyệt qua tất cả các đỉnh có thể.
Stack trong ví dụ này được triển khai bằng cách sử dụng một danh sách đơn giản. Ta sử dụng phương thức pop() để lấy phần tử trên cùng của stack và append() để đẩy phần tử vào stack. kết quả:
>
```
A
C
F
B
E
D
```
## 
- Trong thuật toán tìm kiếm theo chiều rộng (BFS), thường sử dụng hàng đợi (queue) thay vì stack để duyệt qua các đỉnh theo nguyên tắc "First-In-First-Out" (FIFO).
##
- Về mặt tìm kiếm nhị phân, stack có thể được sử dụng để giải quyết bài toán theo nguyên tắc "Divide and Conquer" (chia để trị). Khi thực hiện tìm kiếm nhị phân trên một mảng đã được sắp xếp, ta có thể sử dụng stack để lưu trữ các phạm vi con của mảng và thực hiện tìm kiếm trong phạm vi đó.
```
# ví dụ về tìm kiếm nhị phân trong một mảng sắp xếp bằng cách sử dụng stack 
def binary_search(arr, target):
    left = 0
    right = len(arr) - 1
    stack = [(left, right)]
    
    while stack:
        left, right = stack.pop()
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            if mid + 1 <= right:
                stack.append((mid + 1, right))
        else:
            if mid - 1 >= left:
                stack.append((left, mid - 1))
    
    return -1

# Mảng mẫu đã được sắp xếp
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Tìm kiếm giá trị 6
index = binary_search(arr, 6)
print("Index:", index)
```
> Trong đoạn mã trên, chúng ta sử dụng stack để lưu trữ các phạm vi con của mảng cần tìm kiếm. Ban đầu, ta đẩy phạm vi đầu tiên của mảng (left = 0, right = len(arr) - 1) vào stack. Sau đó, chúng ta thực hiện vòng lặp while cho đến khi stack rỗng. Trong vòng lặp, ta lấy phạm vi trên cùng của stack và tính toán chỉ số giữa (mid). Nếu giá trị tại vị trí mid trùng khớp với giá trị cần tìm, ta trả về chỉ số mid. Nếu giá trị tại vị trí mid nhỏ hơn giá trị cần tìm, ta kiểm tra xem có phạm vi con bên phải của mid không và đẩy nó vào stack nếu có. Ngược lại, nếu giá trị tại vị trí mid lớn hơn giá trị cần tìm, ta kiểm tra xem có phạm vi con bên trái của mid không và đẩy nó vào stack nếu có. Quá trình này tiếp tục cho đến khi ta tìm thấy giá trị cần tìm hoặc stack trở thành rỗng. Ta sử dụng phương thức pop() để lấy phạm vi trên cùng của stack và append() để đẩy phạm vi vào stack.
kết quả:
>
```
Index: 5
```

