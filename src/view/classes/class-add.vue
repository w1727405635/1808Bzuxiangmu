<template>
  <div class="sy">
    <div>
      <p>班级:</p><input class="one" type="text" v-model="bj" />
    </div>

    <div>
      <p>人数:</p><input class="one" type="text" v-model="rs"/>
    </div>

    <div>
      <p>班主任:</p><input class="one" type="text" v-model="bzr"/>
    </div>

    <div>
      <p>任课老师:</p><input class="one" type="text" v-model="rkls"/>
    </div>
    <router-view />
    <button class="zuo" @click="tj">添加一条</button>
    <button class="you">添加多条</button>
  </div>
</template>

<script>
export default {
  data(){
    return{
      bj:'',
      rs:'',
      bzr:'',
      rkls:'',
    }
  },
  methods:{
    tj(){
      //班级名称
      let obj = {
        name: this.bj,
        age: this.rs,
        name1: this.bzr,
        address: this.rkls
      } 
      console.log(obj)
      this.$router.push({path:'/classes/classlist',query:{obj:obj}})
    }
  }
}
</script>

<style>
    .sy{

    }
    .one{
        width: 200px;
        height: 25px;
        margin-left: 50px;
    }
    .zuo{
        margin-left: 50px;
    }
    .you{
        margin-left: 195px;
    }
</style>





git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/w1727405635/1808Bzuxiangmu.git
git push -u origin master