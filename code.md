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
        left = [0] * cots
        right = [cots] * cots

        for hang in range(hangs):
            for cot in range(cots):
                if matrix[hang][cot] == kytu:
                    h[cot] += 1
                else:
                    h[cot] = 0

            left_bound = 0
            for cot in range(cots):
                if matrix[hang][cot] == kytu:
                    left[cot] = max(left[cot], left_bound)
                else:
                    left_bound = cot + 1
                    left[cot] = 0

            right_bound = cots
            for cot in range(cots - 1, -1, -1):
                if matrix[hang][cot] == kytu:
                    right[cot] = min(right[cot], right_bound)
                else:
                    right_bound = cot
                    right[cot] = cots

            for cot in range(cots):
                dientich = h[cot] * (right[cot] - left[cot])
                if dientich > dientich_max:
                    dientich_max = dientich
                    kytu_max = kytu
                    toado_max = [(hang - h[cot] + 1, left[cot]), (hang, left[cot]), (hang, right[cot] - 1), (hang - h[cot] + 1, right[cot] - 1)]

    if dientich_max == 0:
        return None
    else:
        return kytu_max, toado_max

def in_hinhchunhat(matrix, toado_max):
    hangs, cots = len(matrix), len(matrix[0])
    min_hang, min_cot = hangs, cots
    max_hang, max_cot = -1, -1

    for toado in toado_max:
        hang, cot = toado
        min_hang = min(min_hang, hang)
        min_cot = min(min_cot, cot)
        max_hang = max(max_hang, hang)
        max_cot = max(max_cot, cot)

    for hang in range(min_hang, max_hang + 1):
        for cot in range(min_cot, max_cot + 1):
            print(matrix[hang][cot], end=' ')
        print()

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
    for toado in toado_max:
        print(toado)
    print("Ma trận hình chữ nhật:")
    in_hinhchunhat(matrix, toado_max)
else:
    print("Không tìm thấy hình chữ nhật cực đại")

```
