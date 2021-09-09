<template>
  <div>
    <table>
        <thead>
            <tr>
                <th></th>
                <th v-for="item in columnCount" :key="item">{{(item-1)*5}}%</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(item,index) in table" :key="index" >
                <td>{{wiasArr[index]}}%</td>
                <td v-for="(fpa,i) in item" :key="i" >{{fpa}}</td>
            </tr>
        </tbody>
    </table>
      <!-- <div>
          Gear ias: <input type="text" v-model.number="gearIas">
      </div>
      <div>
          WIAS: <input type="text" v-model.number="wias">
      </div> -->
  </div>
</template>

<script>
export default {
    data (){
        return {
            // gearIas:400,
            // wias:200,
            wsm:25,
            columnCount: 15,
            table:[],
            wias: 200,
            wiasArr:[]
        }
    },
    created(){
        // const iasArr = this.generateArray(0);
        // this.wiasArr = this.generateArray(this.wias);
        // this.table = this.wiasArr.map(item => iasArr.map(ias => this.calculateFPA(item, ias)))
        // console.log(this.table)
        console.log(this.calculateFPA(100, 0))
        // gearias包含wias, 變熊多200%ias?, motw也多了20%sias

    },
    methods:{
        calculateFPA(wias, otherIas){
            const gearIas = otherIas + wias + 200;
            const eias = Math.floor(120*gearIas/(120 + gearIas)) + 20;
            const speedModifier = Math.min(eias - this.wsm, 75);
            const e1 = Math.floor((100 + wias - this.wsm)*256/100);
            const delay = Math.floor(256*17/e1);
            const animSpeed = Math.floor(256*7/delay);
            const denominator = Math.floor(animSpeed*(100 + speedModifier)/100);
            console.log({eias})
            console.log({speedModifier})
            console.log({e1})
            console.log({delay})
            console.log({animSpeed})
            console.log({denominator})
            return Math.ceil(12*256/denominator)-1            
        },
        generateArray(begin){
            return Array(this.columnCount).fill(begin).map((item, index)=> item + index*5)
        }
    }
};
</script>

<style>
</style>