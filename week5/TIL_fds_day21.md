# 4/16(월)

## 1. Today I learned

### 1-1. 객체
  


### 1-2. 배열

## 2. Today I found out
  
## 3. Ref
function sort(arr,func){
  return arr.reduce(
  (acc,item) => {
    for(i=0;i<acc.length;i++){
      if(func(item,acc[i]) < 0){
        break;
      }
    }
    acc.splice(i,0,item);
    return acc;
    },
    []
  );   
}

sort([1,3,5,7,8],(x,y) => y-x)