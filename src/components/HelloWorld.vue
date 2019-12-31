<template>
  <div id="todos">
    <input type="text" class="title" :placeholder="msg" v-model="doSome" @keydown.enter="addData" />
    <div class="list" v-for="(item,index) in list" :key="index">
      <input
        type="checkbox"
        class="checkbox"
        :key="index"
        v-model="item.isDone"
        @change="changeIsdone"
      />
      <span :class="item.isDone?'active':''">{{item.title}}</span>
    </div>
    <div class="foot" v-if="yuanshiList!=null||yuanshiList!=[]">
      <span class="total">总共{{all}}</span>
      <span class="left">{{left}}剩余</span>
      <div class="status">
        <span :class="go==index1?'active':''" @click="lookout(index1)" v-for="(item1,index1) in items" :key="index1">{{item1}}</span>
        <!-- <span @click="lookTodo" >未完成</span>
        <span @click="lookDone" >已完成</span>-->
      </div>
      <span class="clear" v-if="all-left" @click="clearDone">清除已完成</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  created() {
    if (localStorage.getItem("todos")) {
      this.list = JSON.parse(localStorage.getItem("todos"));
    }
  },
  computed: {
    activeList() {
      return;
    },
    all() {
      return this.yuanshiList.length;
    },
    left() {
      return this.yuanshiList.filter(ele => {
        return ele.isDone == false;
      }).length;
    }
  },
  data() {
    return {
      doSome: "",
      yuanshiList: JSON.parse(localStorage.getItem("todos")),
      list: [],
      isDone: false,
      isChecked: false,
      items: ["全部", "待办", "已完成"],
      go:0
    };
  },
  methods: {
    // 添加条例
    addData() {
      let add = {
        id: this.list.length,
        title: this.doSome,
        isDone: this.isDone
      };
      this.list.push(add);
      localStorage.setItem("todos", JSON.stringify(this.list));
      this.doSome = "";
      this.yuanshiList = JSON.parse(localStorage.getItem('todos'))
    },
    // 改变完成状态
    changeIsdone() {
      localStorage.setItem("todos", JSON.stringify(this.list));
      this.yuanshiList=JSON.parse(localStorage.getItem('todos'))
    },
    // 清除已完成
    clearDone() {
      let arr = JSON.parse(localStorage.getItem('todos'))
      arr=arr.filter(ele=>{
        return ele.isDone==false
      })
      localStorage.setItem('todos',JSON.stringify(arr))
      this.list = arr
      this.yuanshiList=arr
    },
    // 查看全部
    lookout(idx) {
      this.go=idx
      if (idx == 0) {
        this.list = JSON.parse(localStorage.getItem("todos"));
      } else if (idx == 1) {
        this.list = JSON.parse(localStorage.getItem("todos")).filter(item => {
          return item.isDone == false;
        });
      } else {
        document.addEventListener
        this.list = JSON.parse(localStorage.getItem("todos")).filter(item => {
          return item.isDone == true;
        });
      }
    }
    // 查看待办
    // lookTodo() {
    //   this.list = JSON.parse(localStorage.getItem("todos")).filter(item => {
    //     return item.isDone == false;
    //   });
    //   console.log(this.list);
    // },
    // // 查看已完成
    // lookDone() {
    //   this.list = JSON.parse(localStorage.getItem("todos")).filter(item => {
    //     return item.isDone == true;
    //   });
    // }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
#todos {
  .title {
    width: 400px;
    height: 40px;
    box-sizing: border-box;
    padding-left: 30px;
    &:placeholder-shown {
      font-style: oblique;
      color: #eee;
    }
  }
  .list {
    width: 400px;
    height: 40px;
    line-height: 40px;
    border: 1px solid #ccc;
    margin: 0 auto;
    background-color: #fff;
    text-align: left;
    .active {
      color: #ccc;
      text-decoration: line-through;
    }
  }
  .foot {
    width: 400px;
    height: 20px;
    line-height: 20px;
    font-size: 12px;
    color: #bbb;
    border: 1px solid #ccc;
    background-color: #fff;
    margin: 0 auto;
    .total {
      float: left;
    }
    .left {
      float: left;
      margin-left: 16px;
    }
    .status {
      float: left;
      margin-left: 60px;
      span {
        margin-left: 10px;
        cursor: pointer;
        &.active {
          border: 1px solid blue;
        }
      }
    }
    .clear {
      float: right;
      cursor: pointer;
    }
  }
}
</style>
