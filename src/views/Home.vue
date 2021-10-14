<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld
      :msg="msg"
    />
    <button
      @click="changeMsg"
    >
      change Msg
    </button>
    <hr>
    <div>
      <div>
        {{ shopName }}
      </div>
      <div>
        DOG : {{ dogCnt }}
        <br>
        CAT : {{ catCnt }}
      </div>
      <button
        @click="changePetShopInfo"
      >
        Change Pet Shot Info
      </button>
    </div>
    <hr>
    <reactive-comp
      v-model="reactiveCompVal.cnt"
      v-model:other-text="reactiveCompVal.text"
    />
    <button
      @click="plusOneValue"
    >
      +1
    </button>
    <hr>
    <div>
      123
    </div>
  </div>
</template>

<script>
import { ref, reactive, toRefs } from 'vue';
import HelloWorld from '../components/HelloWorld.vue';
import ReactiveComp from '../components/ReactiveComp.vue';

export default {
  name: 'Home',
  components: {
    ReactiveComp,
    HelloWorld,
  },
  setup() {
    const msg = ref('Welcome to Your Vue.js App');
    const changeMsg = () => {
      msg.value += '1';
    };

    const petShopInfo = reactive({
      shopName: 'animal clinic',
      dogCnt: 3,
      catCnt: 10,
    });
    const changePetShopInfo = () => {
      petShopInfo.dogCnt += 1;
      petShopInfo.catCnt -= 1;
    };

    const reactiveCompVal = reactive({
      cnt: 0,
      text: 'test',
    });
    const plusOneValue = () => {
      reactiveCompVal.cnt += 1;
    };

    return {
      msg,
      ...toRefs(petShopInfo),

      changeMsg,
      changePetShopInfo,

      reactiveCompVal,
      plusOneValue,
    };
  },
};
</script>
