```
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
                    h[cot] +=1
                else:
                    h[cot] = 0
            
            stack = []
            for i in range(cots + 1):
                while stack and (i == cots or h[stack [-1]] > h[i]):
                    a = h[stack.pop()]
                    b = i if not stack else i - stack[-1]-1
                    dientich = a*b
                    if dientich > dientich_max:
                        dientich_max = dientich
                        kytu_max = kytu
                        toado_max = [(cot - a + 1, stack[-1]+1), (hang, stack[-1]+1), (hang, cot), (hang - a + 1,cot)]
                        
                stack.append(i)
                
    if dientich_max == 0:
        return None
    else:
        return kytu_max, toado_max
        
        
    def in_hinhchunhat(matrix, toado_max):
        rows, cols = len(matrix), len(matrix[0])
        min_row, min_col = rows, cols
        max_row, max_col = -1, -1

        for toado in toado_max:
            cot, hang = toado
            min_hang = min(min_hang, hang)
            min_cot = min(min_cot, cot)
            max_hang = max(max_hang, hang)
            max_cot = max(max_cot, cot)

        for hang in range(min_hang, max_hang + 1):
            for col in range(min_col, max_cot + 1):
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
    print("ky tu lon nhat là {}".format(kytu))
    print("Tọa độ 4 điểm của hình chữ nhật:")
    for toado in toado_max:
        print(toado)

```
