<template>
  <div>
      <h3>計算方式</h3>
      <div>原本裝備抗性下受到的傷害100</div>
      <div>提升裝備後受到的傷害80</div>
      <div>那提升的效率就是 (100-80)/100 = 20% </div>
      <br/>
      <div>原本裝備的抗性：</div>
      <div>
          <div>
            <label for="">抗性%：</label>
            <input class="input" type="number" v-model="originResist">              
          </div>
          <div>
            <label for="">元素吸收%：</label>
            <input class="input" type="number" v-model="originAbsorb">              
          </div>
          <div>傷減後所受傷害為{{ toPercent(originReduction) }}%</div>
      </div>
      <br/>
      <div>裝備提升後的抗性：</div>
      <div>
          <div>
            <label for="">抗性%：</label>
            <input class="input" type="number" v-model="betterResist">              
          </div>
          <div>
            <label for="">元素吸收%：</label>
            <input class="input" type="number" v-model="betterAbsorb" >              
          </div>
          <div>傷減後所受傷害為{{ toPercent(betterReduction) }}%</div>
      </div>
      <br/>
      <h4>傷減效率提升{{ toPercent(efficiency) }}%</h4>
      <button class="button" @click="calulate">計算</button>
      <br />
      <br />
      <h3>元素傷減公式:</h3>
      <div>元素抗性%為X</div>
      <div>元素吸收%為Y</div>
      <h4>所受到的元素傷害 = 1 - (法術傷害 - 元素吸收*2) * (1 - X) * (1 - Y*2)</h4>
      <div>這遊戲傷害太高，元素吸收直接忽略不計，公式可以縮寫成</div>
      <div>所受到的元素傷害 = X + 2Y - 2XY</div>      
  </div>
</template>

<script>
export default {
    data(){
        return {
            originResist:75, 
            originAbsorb:5,
            originReduction:0.225,
            betterResist:80, 
            betterAbsorb:5,
            betterReduction:0.18,
            efficiency: 0.20
        }
    },
    methods:{
        calulate(){
            this.originReduction = 1- (this.originResist/100 + 2*this.originAbsorb/100 - 2*this.originResist*this.originAbsorb/10000);
            this.betterReduction = 1- (this.betterResist/100 + 2*this.betterAbsorb/100 - 2*this.betterResist*this.betterAbsorb/10000); 
            this.efficiency = ((this.originReduction - this.betterReduction)/this.originReduction);
        },
        toPercent(num){
            return (num*100).toFixed(2)
        }
    }
};
</script>

<style>
 .button {
    display: inline-block;
    line-height: 1;
    white-space: nowrap;
    cursor: pointer;
    background: #fff;
    border: 1px solid #dcdfe6;
    color: #606266;
    text-align: center;
    box-sizing: border-box;
    outline: none;
    padding: 8px 14px;
    border-radius: 4px;
    color: #fff;
    background-color: #409eff;
    border-color: #409eff;    
 }
 .input {
    background-color: #fff;
    background-image: none;
    border-radius: 4px;
    border: 1px solid #dcdfe6;
    box-sizing: border-box;
    color: #606266;
    display: inline-block;
    height: 30px;
    line-height: 30px;
    outline: none;
    padding: 0 10px;
    margin: 3px 0;
 }
</style>
