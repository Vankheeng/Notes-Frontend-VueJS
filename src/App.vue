<script setup>
  import{ref} from "vue";

  const showModal = ref(false);
  const newNote = ref("")
  const errorMessage = ref("")
  const notes = ref([])

  function getRandomColor(){
    return "hsl(" + Math.random() * 360 + ", 100%, 75%";
  }

  const addNote = () =>{
    if(newNote.value.trim.length < 10) {
      return errorMessage.value = "Note needs to be 10 characters or more "
    }
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor()
    })
    showModal.value = false
    newNote.value = ""
    errorMessage = ""
  }

  // const 
</script>
<template>
  <main>
    <!-- v-if loai bo hoan toan html element -->
     <!-- v-show chuyen trang thi cua display = none de an di -->
    <div v-show= "showModal" class="overlay">
      <div class="modal">
        <!-- Liên kết hai chiều giữa nội dung trong ô và biến newNote -->
        <textarea v-model = "newNote" name="note" id="note" cols=" 30" rows=" 10"></textarea>
        <p v-if = "errorMessage"> {{errorMessage}}</p>
        <button @click = "addNote" >Add Note</button>
        <button @click = "showModal = false" class="close">Close</button>
      </div>
    </div> 
    <div class="container">
      <header>
        <h1>Notes </h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div 
          v-for="note in notes" 
          :key = "note.id"
          class="card" 
          :style="{backgroundColor: note.backgroundColor}"
          >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-us") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scope>
  main{
    height: 100vh;
    width: 100vw;
  }
  .container{
    max-width: 1000px;
    padding:  10px;
    margin: 0 auto;
  }

  header{

    /* thành một container flexbox, cho phép các phần tử con bên trong được sắp xếp theo một trục (ngang hoặc dọc). */
    display: flex; 
    /* Phân phối các phần tử con theo chiều ngang với khoảng cách bằng nhau giữa chúng. Phần tử đầu tiên sẽ dính bên trái, phần tử cuối cùng sẽ dính bên phải, và khoảng trống giữa các phần tử sẽ được phân bổ đều. */
    justify-content: space-between;
    /* Căn các phần tử con theo chiều dọc sao cho chúng được căn giữa theo trục dọc (theo chiều cao của container). */
    align-items: center;

  }

  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  header button{
    border:  none;
    padding:  10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(21, 20, 20);
    border-radius: 100%;
    color: white;
    font-size: 20px;
  }

  .card{
    width: 225px;
    height: 225px;
    background-color:  rgb(237, 182, 44);
    padding: 10px;
    border-radius:  15px;
    flex-direction:  column;
    justify-content: space-between;
    margin-left: 20px;
    margin-right: 20px;
  }
  .date{
    font-size: 12.5px;
    font-weight: bold;
  }
  
  .cards-container{
    /* Điều này cho phép các phần tử con (thẻ) được sắp xếp theo hàng hoặc cột linh hoạt. */
    display: flex; 
    /* Cho phép các phần tử con tự động xuống dòng nếu không đủ không gian trên cùng một hàng. */
    flex-wrap: wrap;
  }

  .overlay{
    /* Định vị phần tử theo các giá trị top, left, right, và bottom dựa trên phần tử chứa gần nhất có thuộc tính position */
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    /* Đặt phần tử này ở lớp trên cùng, cao hơn những phần tử có z-index thấp hơn */
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal{
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;

  }

  .modal button{
    padding: 10px 20px;
    font-size:  20px;;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }

  .modal .close{
    background-color: red;
    margin-top: 7px;
  }

  .modal p{
    color: red
  }

</style>