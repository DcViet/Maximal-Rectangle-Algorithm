```python
def tim_hinhchunhat_toidai(matrix, kytu):
    hangs = len(matrix)
    if hangs == 0:
        return None
    
    cots = len(matrix[0])
    
    dientich_max = 0
    toado_max = []
    
    for hang in range(hangs):
        for cot in range(cots):
            if matrix[hang][cot] == kytu:
                min_hang, min_cot = hang, cot
                max_hang, max_cot = hang, cot
                for i in range(hang, hangs):
                    if matrix[i][cot] != kytu:
                        break
                    max_hang = i
                for j in range(cot, cots):
                    if matrix[hang][j] != kytu:
                        break
                    max_cot = j
                dientich = (max_hang - min_hang + 1) * (max_cot - min_cot + 1)
                if dientich > dientich_max:
                    dientich_max = dientich
                    toado_max = [(min_hang, min_cot), (max_hang, min_cot), (max_hang, max_cot), (min_hang, max_cot)]
    
    if dientich_max == 0:
        return None
    else:
        return dientich_max, toado_max


matrix = [
    "bbsbmaacccaabbfbbbb",
    "mbvhbcccccccbbgbbvb",
    "xbkkbcccccccbbgbvvb",
    "cbhbbcccccccbbtbxxb",
    "vbmbbcccccccbbtrrbb",
    "zbnbbcccccccbbtqqbb"
]

kytu = 'c'

result = tim_hinhchunhat_toidai(matrix, kytu)
if result is not None:
    dientich, toado_max = result
    print("Ma trận ban đầu:")
    for hang in matrix:
        print(hang)
    
    print("\nThông tin về hình chữ nhật cực đại tương ứng với ký tự '{}':".format(kytu))
    print("Diện tích: {}".format(dientich))
    print("Vị trí các đỉnh:")
    for i, toado in enumerate(toado_max):
        hang, cot = toado
        print("Đỉnh {}: Hàng {}, Cột {}".format(i+1, hang+1, cot+1))
else:
    print("Không tìm thấy hình chữ nhật cực đại tương ứng với ký tự '{}'".format(kytu))
    
```
