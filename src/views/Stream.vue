<template>
  <div>
    <div class="mb">
   
    </div>
    <div class="center stream">
      <qr-stream @decode="onDecode" class="mb">
        <div style="color: red;" class="frame"></div>
      </qr-stream>

      <!-- <div @click="onDecode('6565ba3fce92e')" style="cursor: pointer;background-color: red;"> Click</div> -->
    </div>
    <!-- <div class="result">
      Result: {{data}}
    </div> -->
  </div>
</template>
    
    <script>
import { reactive, toRefs, watch } from 'vue';

// @ is an alias to /src
import { QrStream } from 'vue3-qr-reader';
import router from '@/router';

export default {
  name: "HomeView",
  components:{QrStream},
  setup() {
    const state = reactive({
      data: null
    })
    const  onDecode=(data) =>{
      state.data = data
    }

    watch(state,()=>{

      if(state.data){
        const parts = state.data.split('/');
        const lastElement = parts[parts.length - 1];

        if(lastElement){
          router.push({name:'details',params:{id:lastElement}})

        }else{
          router.push({name:'details',params:{id:0}})

        }

       
      }

    })
    return {
      ...toRefs(state),
      onDecode
    }
  }
};
</script>
    
<style scoped>
.stream {
  max-height: 500px;
  max-width: 500px;
  margin: auto;
}
.frame {
  border-style: solid;
  border-width: 2px;
  border-color: red;
  height: 200px;
  width: 200px;
  position: absolute;
  top: 0px;
  bottom: 0px;
  right: 0px;
  left: 0px;
  margin: auto;
}
</style>