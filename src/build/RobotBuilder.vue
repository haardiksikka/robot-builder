<template>
  <div class="content">
     <div class="preview">
       <p>Sample Preview of your bot</p>
      <div class="preview-content" :title="selectedRobot.head.title">
        <div class="top-row">
          <img :src="selectedRobot.head.src"/>
        </div>
        <div class="middle-row">
          <img :src="selectedRobot.leftArm.src" class="rotate-left"/>
          <img :src="selectedRobot.torso.src"/>
          <img :src="selectedRobot.rightArm.src" class="rotate-right"/>
        </div>
        <div class="bottom-row">
          <img :src="selectedRobot.base.src"/>
        </div>
      </div>
       <button class="add-to-cart" @click="addToCart()">Add To Cart</button>
    </div>
   
    <div class="top-row">
      <!-- <div class="top part"> -->
        <!-- <div class="robot-head">{{availableParts.heads[headIndex].title}}</div> -->
        <!-- <img v-bind:src="availableParts.heads[headIndex].src" title="head">
        <button class="prev-selector" v-on:click="selectPreviousHead()">&#9668;</button>
        <button class="next-selector" v-on:click="selectNextHead()">&#9658;</button> -->
        <PartSelector :parts="availableParts.heads" position="top" @partSelected="part => selectedRobot.head=part"/>
      <!-- </div> -->
    </div>
    <div class="middle-row">
      <!-- <div class="left part">  -->
        <!-- <img v-bind:src="availableParts.arms[armIndex].src" title="left arm">
        <button class="prev-selector" v-on:click="selectPreviousArm()">&#9650;</button>
        <button class="next-selector" v-on:click="selectNextArm()">&#9660;</button> -->
        <PartSelector :parts="availableParts.arms" position="left" @partSelected="part => selectedRobot.leftArm=part"></PartSelector>
       <!-- </div>  -->
      <!-- <div class="center part"> -->
        <!-- <img v-bind:src="availableParts.torsos[torsoIndex].src" title="left arm">
        <button class="prev-selector" v-on:click="selectPreviousTorso()">&#9668;</button>
        <button class="next-selector" v-on:click="selectNextTorso()">&#9658;</button> -->
        <PartSelector :parts="availableParts.torsos" position="center" @partSelected="part => selectedRobot.torso=part"></PartSelector>
      <!-- </div>
      <div class="right part"> -->
        <!-- <img v-bind:src="availableParts.arms[armIndex].src" title="left arm">
        <button class="prev-selector" v-on:click="selectPreviousArm()">&#9650;</button>
        <button class="next-selector" v-on:click="selectNextArm()">&#9660;</button> -->
        <PartSelector :parts="availableParts.arms" position="right" @partSelected="part => selectedRobot.rightArm=part"></PartSelector>
      <!-- </div> -->
    </div>
     <div class="bottom-row">
      <!-- <div class="bottom part"> -->
        <!-- <img v-bind:src="availableParts.bases[baseIndex].src" title="left arm">
        <button class="prev-selector" v-on:click="selectPreviousBase()">&#9668;</button>
        <button class="next-selector" v-on:click="selectNextBase()">&#9658;</button> -->
        <PartSelector :parts="availableParts.bases" position="bottom" @partSelected="part => selectedRobot.base=part"></PartSelector>
      <!-- </div> -->
    </div>
    <div class="cart">
      <h1 style="text-align:left"> Cart </h1> 
      <table border="1px">
        <thead>
          <tr>
            <th>Robot Name</th>
            <th>Robot Cost</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item,index) in cart" :key="index">
            <td>{{item.robot.title}}</td>
            <td>{{item.cartTotal}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>


<script>
import availableParts from "../data/part.js";
import PartSelector from "./partSelector.vue";
//helper methods cant accessed in html/view
// function select(){
//   body
// }

// everything inside this can be accessed in html/view
export default {
  name: "RobotBuilder",
  components:{PartSelector},
  data() {
    return {
      availableParts,
      cart: [],
      selectedRobot:{
        head:{},
        leftArm:{},
        rightArm:{},
        base:{},
        torso:{},
      }
      // headIndex: 0,
      // armIndex: 0,
      // torsoIndex: 0,
      // baseIndex: 0
    };
  },

  methods: {
    // selectNextHead() {
    //   console.log(this.headIndex);
    //   if (this.headIndex + 1 < availableParts.heads.length) this.headIndex += 1;
    //   else {
    //     this.headIndex = 0;
    //   }
    // },
    // selectPreviousHead() {
    //   if (this.headIndex - 1 >= 0) {
    //     this.headIndex -= 1;
    //   } else {
    //     this.headIndex = availableParts.heads.length - 1;
    //   }
    // },
    // selectNextArm() {
    //   if (this.armIndex + 1 < availableParts.arms.length) this.armIndex += 1;
    //   else {
    //     this.armIndex = 0;
    //   }
    // },
    // selectPreviousArm() {
    //   if (this.armIndex - 1 >= 0) {
    //     this.armIndex -= 1;
    //   } else {
    //     this.armIndex = availableParts.arms.length - 1;
    //   }
    // },
    // selectNextBase() {
    //   console.log(this.baseIndex);
    //   if (this.headIndex + 1 < availableParts.bases.length) this.baseIndex += 1;
    //   else {
    //     this.baseIndex = 0;
    //   }
    // },
    // selectPreviousBase() {
    //   if (this.baseIndex - 1 >= 0) {
    //     this.baseIndex -= 1;
    //   } else {
    //     this.baseIndex = availableParts.bases.length - 1;
    //   }
    // },

    // selectNextTorso() {
    //   console.log(this.torsoIndex);
    //   if (this.torsoIndex + 1 < availableParts.torsos.length) {
    //     this.torsoIndex += 1;
    //   } else {
    //     this.torsoIndex = 0;
    //   }
    // },
    // selectPreviousTorso() {
    //   if (this.torsoIndex - 1 >= 0) {
    //     this.torsoIndex -= 1;
    //   } else {
    //     this.torsoIndex = availableParts.torsos.length - 1;
    //   }
    // },
    addToCart() {
      // const robot = availableParts.heads[this.headIndex];
      // const cartTotal =
      //   availableParts.heads[this.headIndex].cost +
      //   2 * availableParts.arms[this.armIndex].cost +
      //   availableParts.torsos[this.torsoIndex].cost +
      //   availableParts.bases[this.baseIndex].cost;

      // this.cart.push(Object.assign({ robot }, { cartTotal }));
    console.log(this.selectedRobot.rightArm.cost)
    const robot = this.selectedRobot.head;
    const cartTotal = this.selectedRobot.head.cost
                     + this.selectedRobot.leftArm.cost
                     + this.selectedRobot.rightArm.cost
                     + this.selectedRobot.torso.cost
                     + this.selectedRobot.base.cost;
     console.log(cartTotal);
     this.cart.push(Object.assign({robot},{cartTotal}));
    }
  }
};
</script>


<style>
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;
}
.part img {
  width: 165px;
}
.top-row {
  display: flex;
  justify-content: space-around;
}
.middle-row {
  display: flex;
  justify-content: center;
}
.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
.robot-head {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
.content {
  position: relative;
}
.add-to-cart {
  position: absolute;
  font-size: 16px;
  width:210px;
  right:5px;
  
}
.preview {
  position: absolute;
  top: -20px;
  right: 0;
  width: 210px;
  height: 210px;
  padding: 5px;
}
.preview-content {
  border: 1px solid #999;
}
.preview img {
  width: 50px;
  height: 50px;
}
.rotate-right {
  transform: rotate(90deg);
}
.rotate-left {
  transform: rotate(-90deg);
}

</style>
