<template>
  <div class="">
    <Checkbox
    @click.prevent.native="handleCheckAllCountryArea"
    v-model="checkAllCountryArea"
    >全选</Checkbox>
    <div class="ChecboxList">
      <Checkbox :key="k" :value="(PickCountryArea.indexOf(item.countryNameCN)>=0) ? true : false" @on-change="checkAllGroupChangeForCountryArea(item.countryNameCN, PickCountryArea.indexOf(item.countryNameCN))" v-for="(item, k) in AreaList">{{item.countryNameCN}}</Checkbox>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      checkAllCountryAreaBtn:false,
      pickArrayCounterArea:this.AreaList,
    }
  },
  props:{
    AreaList: {
      type: Array,
      default: []
    },
    PickCountryArea:{
      type: Array,
      default: []
    }
  },
  computed:{
    checkAllCountryArea(){
      if(this.AreaList.length === this.GroupCountryArea.length){
        this.checkAllCountryAreaBtn = true;
        return true;
      }else{
        this.checkAllCountryAreaBtn = false;
        return false;
      }
    },
    GroupCountryArea(){
      const arr = [];
      this.AreaList.forEach((item)=>{
        let i = this.PickCountryArea.indexOf(item.countryNameCN);
        if(i>-1){
          arr.push(item.countryNameCN)
        }
      });
      return arr;
    }
  },
  methods:{
    checkAllGroupChangeForCountryArea(data, pick){
      this.$emit('on-change', [data, pick]);
    },
    handleCheckAllCountryArea(){
      if(!this.checkAllCountryAreaBtn){
        this.AreaList.forEach((item)=>{
          const i = this.PickCountryArea.indexOf(item.countryNameCN)
          if(i==-1){
            this.$emit('on-change', [item.countryNameCN, i]);
          }
        });
      }else{
        this.AreaList.forEach((item)=>{
          const i = this.PickCountryArea.indexOf(item.countryNameCN)
          if(i>-1){
            this.$emit('on-change', [item.countryNameCN, i]);
          }
        });
      }
    },
  }
}
</script>

<style lang="css">
  .ChecboxList{
    white-space: normal;
    height: 140px;
  }
</style>
