// function print() {
  
//   for(var i =1; i<=5; i++){
//     function printNumber(i){
//       setTimeout(function() {
//         console.log(i)
//       }, i * 1000);
//     }
//     printNumber(i)
//   }

  
// }

// print()

// callstack 


// Input: [1,2,3,[4,5],[[6]]]
// Output: [1,2,3,4,5.[6]]

if(!Array.prototype.flat){
    Array.prototype.flat = function () {
        let array = this 
        let newArray = [];
        
        function flat (array) {
            for(let i =0; i<array.length; i++){
          
                if(Array.isArray(array[i])){
                    flat(array[i])
                }
                newArray.push(array[i])
            }
            
         return newArray;   
            
        }
        
        let result = flat(array)
        return result 
    }
}

console.log([1,2,3,[4,5],[[6]]].flat())

[
  {
    name: 'A',
    specs: {
      battery: '1500mah',
      size: '6inch'
    }
  }, 
  {
    name: 'B',
    specs: {
      version: '2',
      size: '6inch'
    }
  }, 
  {
    name: 'C',
    specs: {
      version: '5',
      color: 'blue'
    }
  }, 
  {
    name: 'D',
    specs: {
      battery: '1200mah',
      size: '4inch'
    }
  }
]
