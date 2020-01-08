1. Tuliskan hasil dari console.log dari code block di bawah dan jelaskan!  
`if(true){    
    let first = 1;  
}  
if(true){    
    var second = 10;  
} `
 
  console.log(first); // Pertanyaan 1  
  console.log(second); // Pertanyaan 2 
  
  Jawaban:
  1. `"ReferenceError: first is not defined"` karena `let` hanya bisa digunakan didalam scope `function` yang sama. Pada kasus ini, `first` didefinisikan pada scope kondisional pertama namun dipakai diluar kondisional yang menghasilkan `ReferenceError`
  2. `10` karena `var` mendefinisikan variable sebagai global variabel yang bisa digunakan diseluruh komponen.