```python
def tim_hinhchunhat_toidai(matrix):
    hangs = len(matrix)
    if hangs == 0:
        return None
    
    cots = len(matrix[0])
    
    dientich_max = 0
    kytu_max = ''
    toado_max = []
    
    for kytu in set(''.join(matrix)):
        h = [0] * cots
        for hang in range(hangs):
            for cot in range(cots):
                if matrix[hang][cot] == kytu:
                    h[cot] += 1
                else:
                    h[cot] = 0
            
            stack = []
            i = 0
            while i < cots:
                if not stack or h[stack[-1]] <= h[i]:
                    stack.append(i)
                    i += 1
                else:
                    top = stack.pop()
                    dientich = h[top] * (i if not stack else i - stack[-1] - 1)
                    if dientich > dientich_max:
                        dientich_max = dientich
                        kytu_max = kytu
                        toado_max = [(hang - h[top] + 1, top), (hang - h[top] + 1, i - 1), (hang, top), (hang, i - 1)]
        
    if dientich_max == 0:
        return None
    else:
        return kytu_max, toado_max


matrix = [
    "bbsbmaacccaabbfbbbb",
    "mbvhbcccccccbbgbbvb",
    "xbkkbcccccccbbgbvvb",
    "cbhbbcccccccbbtbxxb",
    "vbmbbcccccccbbtrrbb",
    "zbnbbcccccccbbtqqbb"
]

result = tim_hinhchunhat_toidai(matrix)
if result is not None:
    kytu, toado_max = result
    print("Ký tự lớn nhất là '{}'".format(kytu))
    print("Tọa độ 4 điểm của hình chữ nhật:")
    for i, toado in enumerate(toado_max):
        hang, cot = toado
        print("Điểm {}: Hàng: {}, Cột: {}".format(i+1, hang+1, cot+1))
        
    print("Ma trận hình chữ nhật cực đại:")
    min_hang, min_cot = toado_max[0]
    max_hang, max_cot = toado_max[0]
    for toado in toado_max:
        hang, cot = toado
        min_hang = min(min_hang, hang)
        min_cot = min(min_cot, cot)
        max_hang = max(max_hang, hang)
        max_cot = max(max_cot, cot)
    
    for hang in range(min_hang, max_hang+1):
        for cot in range(min_cot, max_cot+1):
            print(matrix[hang][cot], end=' ')
        print()
else:
    print("Không tìm thấy hình chữ nhật cực đại.")
```
