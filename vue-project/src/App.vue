<!-- <script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'

</script> -->

<script>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'

export default{
  data() {
    return{
      isShow: true,
      isDisplay: 0,
      list: '',
      todoLists: [],
      studentLists:
      [
        {name: 'Hoang', selected: false, side: 'left'},
        {name: 'Hieu', selected: false, side: 'left'},
        {name: 'Tu', selected: false, side: 'left'},
        {name: 'Huy', selected: false, side: 'right'},
        {name: 'Thuan', selected: false, side: 'right'},
        {name: 'Khoa', selected: false, side: 'right'},
      ],
    }
  },
  methods: {
    addtodoList() {
      this.todoLists.push(this.list);
      this.list = '';
      if (this.todoLists.length > 2) {
        this.isShow = false;
      }
    },
    deltodoList(index) {
      this.todoLists.splice(index, 1);
    },
    removeAll(){
      this.todoLists = [];
      this.isShow = true;
    },
    active(){
      this.colorText = !this.colorText;
    },
    leftChange(){
      this.studentLists.filter(student => student.selected)
      .forEach(student => {
        student.side = 'right';
        student.selected = false;
      })
    },
    rightchange(){
      this.studentLists.filter(student => student.selected)
      .forEach(student => {
        student.side = 'left';
        student.selected = false;
      })
    }  
  },
  mounted() {
  }
}

</script>


<template>
  
  <!-- <header>

    <div class="wrapper">
      <HelloWorld msg="You did it!" />

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header> -->




<!--VuejS -->
  <div id="wrapper">
    <div class="content">
      <h2>Welcome to Lap Trinh Va Cuoc Song </h2>
      <h3>Fullstack 8</h3>
      <ul>
        <li>
          <a href="#" @click.prevent.stop="isDisplay = 1">Bai tap 1</a>
        </li>
        <li>
          <a href="#" @click.prevent.stop="isDisplay = 2">Bai tap 2</a>
        </li>
        <li>
          <a href="#" @click.prevent.stop="isDisplay = 3">Bai tap 3</a>
        </li>
      </ul>

      <div class="modal" v-show="isDisplay == 1" @click="isDisplay = 0">
        <div class="modalContainer" @click.prevent.stop="">
          <div class="modalHeader">
            <p>Welcome to LTVCS FullStack 8</p>
          </div>
          <div class="modalContent">
            <h3>Modal Layer</h3>
            <p>Modal Content</p>
          </div>
        </div>
      </div>

      <div class="modal" v-show="isDisplay == 2" @click="isDisplay = 0">
        <div class="modalContainer" @click.prevent.stop="">
          <div class="modalHeader">
            <p>Todo App</p>
          </div>
          <div class="todolistContent">
            <div class="todolistHeader">
              <input type="text" placeholder="Add your new todo" v-model="list">
              <button @click="addtodoList">Add</button>
            </div>
            <ul class="todoLists">
              <li v-for="(item, index) in todoLists" :key="index">
                <p>
                  {{ item }}
                  <button @click="deltodoList(index)">Del</button>
                </p>
                
              </li>
            </ul>
            <button @click="removeAll" :class="{hide: isShow, show: isShow == false}">Remove all</button>
          </div>
        </div>
      </div>

      <div class="modal" v-show="isDisplay == 3" @click="isDisplay = 0">
        <div class="modalContainer" @click.prevent.stop="">
          <div class="modalHeader">
            <p>Change Student</p>
          </div>
          <div class="studentList">
            <ul>
              <li 
                v-for="(item, index) in studentLists.filter(s => s.side == 'left')" :key="index"
                @click="item.selected = !item.selected"
                :class="{selected: item.selected}"
                >
                <p>
                  {{ item.name }}
                </p>
              </li>
            </ul>
            <button @click="leftChange">Left</button>
            <button @click="rightchange">Right</button>
            <hr>
            <ul>
              <li 
                v-for="(item, index) in studentLists.filter(s => s.side == 'right')" :key="index"
                @click="item.selected = !item.selected"
                :class="{selected: item.selected}"
                >
                <p>
                  {{ item.name }}
                </p>
              </li>
            </ul>
          </div>
        </div>
      </div>

    </div>
  </div>

  <!-- <RouterView /> -->
</template>

<style scoped>

#wrapper{
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: #861657;
  background-image: linear-gradient(326deg, #861657 0%, #ffa69e 74%);
  display: flex;
  align-items: center;
  justify-content: center;
}

.content{


}

.content h2{
  font-size: 40px;
}

.content h3{
  font-size: 24px;
}

.content ul{
  padding: 0;
  margin: 12px 0;
}

.content ul li{
  list-style: none;
  display: inline-block;

}
.content ul li a:first-child{
  margin-left: 0;
}
.content ul li a{
  border-radius: 8px;
  display: block;
  font-size: 24px;
  background: #3333;
  margin: 0 12px;
  color: white;
  padding: 6px 12px;
}

.modal{
  top: 0;
  left: 0;
  position: fixed;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modalContainer{
  position: relative;
  z-index: 999;
  background: white;
  border-radius: 12px;
  overflow: hidden;
}

.modalHeader{
  background-color: #7ee8fa;
  background-image: linear-gradient(315deg, #7ee8fa 0%, #80ff72 74%);

}

.modalHeader p{
  padding: 24px;
  font-size: 24px;
}

.modalContent{
  padding: 24px;
}

/* todo List */
.todolistContent{
  padding: 12px 24px;
}

.todolistHeader{
  display: flex;
  align-items: center;
}

.todolistHeader input{
  flex: 1;
  padding: 12px 10px;
  border-radius: 8px;
  outline: none;
  border: 1px solid #333;
}

.todolistHeader button{
  margin-left: 8px;
  background: #7ee8fa;
  padding: 12px 10px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}

.todoLists{

}

.todoLists li {
  margin: 4px 0;
  width: 100%;
} 

.todoLists li p{
  background: #333;
  color: white;
  padding: 12px 10px;
  border-radius: 8px;
  position: relative;
  font-size: 18px;
}

.todoLists li button{
  position: absolute;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
  padding: 12px;
  border-radius: 8px;
  cursor: pointer;
  background: #d61132;
  color: white;
  border: none;
  outline: none;
  margin-right: 4px ;
}

.show{
  display: block;
  padding: 10px;
  border-radius: 8px;
  background: #10c796;
  cursor: pointer;
  border: none;
  outline: none;
}

.hide{
  display: none;
}

.studentList{
  display: flex;
  align-content: center;
  justify-content: space-between;
  padding: 24px;
  max-width: 500px;
}

.studentList ul:first-child{
  margin-right: 4px;
}

.studentList ul:last-child{
  margin-left: 4px;
}

.studentList ul{
  background: #c9c9c9;
  color: white;
  margin-right: 4px;
  border-radius: 8px;
}

.studentList ul li{
  display: inline-block;
  color: black;
  margin:  4px 8px;
  font-size: 24px;
  background: transparent;
  padding: 4px 8px;
}

.studentList ul li:hover{
  opacity: 0.5;
  cursor: pointer;
}

.selected{
  background: #62f08d !important;
  border-radius: 8px;
  padding: 4px 8px;
}


</style>
