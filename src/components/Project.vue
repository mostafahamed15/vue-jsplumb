<template>
    <el-container class="container" id="work-container">
      <el-aside width="200px">
        <div class="box-card">
            <div class="header">Actions</div>
            <div class="card-body">
            <start  :key="startKey" @forceRerender="forceRerender" :user ="user"></start>
            <callaction :key="callActionKey" @forceRerender1="forceRerender1"></callaction>
            <callinputaction :key="callInputActionKey" @forceRerender2="forceRerender2"></callinputaction>
            <playsoundaction :key="playSoundActionKey" @forceRerender3="forceRerender3"></playsoundaction>
            
            </div>
        </div>
      </el-aside>
      <el-main>
        <div class="workplace" id="workplace">
          </div>
      
      </el-main>
    </el-container>
</template>
<script>
import start from './Start';
import callinputaction from './CallInputAction';
import playsoundaction from './PlaySoundAction';
import callaction from './CallAction';

export default {
   name: 'Project',
  components: {
    start,
    callaction,
    callinputaction,
    playsoundaction
  },
   data() {
    return {
      startKey: 0,
      callActionKey: 0,
      callInputActionKey: 0,
      playSoundActionKey: 0,
      user: "Mostafa"
    };
  },
  methods: {
 
    forceRerender() {
      this.startKey++;
    },
    forceRerender1() {
      this.callActionKey++; 
      console.log(this.callActionKey)
    },
    forceRerender2() {
      this.callInputActionKey++;
      
    },
    forceRerender3() {
        this.playSoundActionKey++  
    }
  
  }
 
}
</script>
<style scoped>
.el-aside {
    background-color: #D3DCE6;
    color: #333;
}
.workplace {
  width: 100%;
  height: 100%;
  position: relative;
}

.title-word {
  list-style: none;
  padding-top: 9px !important;
}

.title-word li::before {
  content: "\2022";
  color: red;
  font-weight: bold;
  display: inline-block; 
  width: 1em;
  margin-left: -1em;
}


</style>