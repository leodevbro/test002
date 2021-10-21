# 1)
![1_1](https://user-images.githubusercontent.com/54504880/138188023-db36eaf6-bf07-42a2-9214-e722e1fbdd66.png)
![1_2](https://user-images.githubusercontent.com/54504880/138188036-5508a024-90f0-4f5a-a2a6-d98f43ff68bd.png)
![1_3](https://user-images.githubusercontent.com/54504880/138188038-210402c5-c115-4772-af1f-73edb9274818.png)

```typescript
// 1)
// A.length >= 5
const requestHandler = (A: number[]): boolean => {
    const len = A.length;
    for (let i = 1; i <= len - 4; i += 1) {
        for (let j = i + 2; j <= len - 2; j += 1) {
            const sub1sum = A.slice(0, i).reduce((a, b) => a + b);
            const sub2sum = A.slice(i + 1, j).reduce((a, b) => a + b);
            const sub3sum = A.slice(j + 1, len).reduce((a, b) => a + b);

            if (sub1sum === sub2sum && sub1sum === sub3sum) return true;
        }
    }

    return false;
};
```


# 2)
![2_1](https://user-images.githubusercontent.com/54504880/138188126-f07032db-c137-41b5-9ff7-0bef8db4396c.png)
![2_2](https://user-images.githubusercontent.com/54504880/138188129-68ef8c92-8298-4387-ace1-1a2a3efd2aca.png)
![2_3](https://user-images.githubusercontent.com/54504880/138188133-6cb5a03e-853f-41b6-afeb-baade969d5f1.png)

```typescript
// 2)
const matrixReverseEngineer = (U: number, L: number, C: number[]): string => {
    const len = C.length;

    let ansSub1: string = "";
    let ansSub2: string = "";

    if (U > len || L > len) return "IMPOSSIBLE";

    for (let i = 0; i < len; i += 1) {
        const nextLen = len - i - 1;

        if (C[i] === 0) {
            if (U <= nextLen && L <= nextLen) {
                ansSub1 += "0";
                ansSub2 += "0";
            } else {
                return "IMPOSSIBLE";
            }
        } else if (C[i] === 2) {
            ansSub1 += "1";
            ansSub2 += "1";

            if (U >= 1 && L >= 1) {
                U -= 1;
                L -= 1;
            } else {
                return "IMPOSSIBLE";
            }
        } else {
            if (U <= nextLen && L >= 1) {
                ansSub1 += "0";
                ansSub2 += "1";
                L -= 1;
            } else if (L <= nextLen && U >= 1) {
                ansSub1 += "1";
                ansSub2 += "0";
                U -= 1;
            } else {
                return "IMPOSSIBLE";
            }
        }
    }

    return ansSub1 + "," + ansSub2;
};

console.log(matrixReverseEngineer(3, 2, [2, 1, 1, 0, 1]));
console.log(matrixReverseEngineer(2, 3, [0, 0, 1, 1, 2]));
console.log(matrixReverseEngineer(2, 2, [2, 0, 2, 0]));
```


# 3)
![3_1](https://user-images.githubusercontent.com/54504880/138188187-e3c38a3f-a0e1-4e5e-b595-d6b3aa468003.png)
![3_2](https://user-images.githubusercontent.com/54504880/138188195-6c5d9b8e-f33c-4462-8316-483589749446.png)
![3_3](https://user-images.githubusercontent.com/54504880/138188203-1fa48997-786f-4ed4-804e-418a734cd9f6.png)

```typescript
// 3)
const findIntegerPoint = (
    AX: number,
    AY: number,
    BX: number,
    BY: number
): string => {
    if (AX === BX) {
        if (BY > AY) {
            return [BX + 1, BY].join(",");
        } else {
            return [BX - 1, BY].join(",");
        }
    } else if (AY === BY) {
        if (BX > AX) {
            return [BX, BY - 1].join(",");
        } else {
            return [BX, BY + 1].join(",");
        }
    }

    const slope = Math.abs((AX - BX) / (AY - BY)); // after turn right

    let dir: [-1 | 1, -1 | 1] | null = null; // after turn right

    if (BX > AX && BY > AY) {
        dir = [1, -1];
    } else if (BX < AX && BY > AY) {
        dir = [1, 1];
    } else if (BX < AX && BY < AY) {
        dir = [-1, 1];
    } else {
        dir = [-1, -1];
    }

    let xCoord = BX;
    let yCoord = BY;

    let count = 0;
    while (count < 10 ** 4) {
        count += 1;
        xCoord += dir[0];
        yCoord = BY + count * dir[1] * slope;

        if (Number.isInteger(yCoord)) {
            break;
        }
    }

    return [xCoord, yCoord].join(",");
};

console.log(findIntegerPoint(-1, 3, 3, 1)); // "2,-1"
console.log(findIntegerPoint(2, 2, 2, -3)); // "1,-3"
console.log(findIntegerPoint(-2, 1, 0, 2)); // "1,0"
console.log(findIntegerPoint(2, 0, 1, -2)); // "-1,-1"
```


```python
# დათას კოდი
def solution(AX, AY, BX, BY):
    x_abs = abs(AX - BX)
    y_abs = abs(AY - BY)

    CX = BX - y_abs
    CY = BY - x_abs

    k = (CY - BY)/(CX - BX)
    b = CY - k*CX

    ret_x = 0
    ret_y = 0

    if CY < BY:
        for y in range(BY-1, CY-1, -1):
            x = (y - b)/k
            if x%1 == 0: return int(x), int(y)
    else:
        for x in range(BX-1, CX-1, -1):
            y = k*x + b
            if y%1 == 0: return int(x), int(y)
    return ret_x, ret_y
```
