<template>
  <div style="width: 500px">
    <a-radio-group v-model:value="mode" :style="{ marginBottom: '8px' }">
      <a-radio-button value="top">Horizontal</a-radio-button>
      <a-radio-button value="left">Vertical</a-radio-button>
    </a-radio-group>
    <a-tabs
        :tab-position="mode"
        :style="{ height: '200px' }"
        @prevClick="callback"
        @nextClick="callback"
        @tabClick="callback"
        v-model:activeKey="activeKey"
    >
      <a-tab-pane v-for="i in 30" :key="i+'key'" :tab="`Tab-${i}`">
        <a-tabs
            :tab-position="mode"
            :style="{ height: '200px' }"
            @prevClick="subCallback"
            @nextClick="subCallback"
            @tabClick="subCallback"
            v-model:activeKey="subActiveKey"
        >
          <a-tab-pane v-for="s in 10" :key="i+':'+s+'subkey'" :tab="`Tab-${s}`">
            Content of tab sub {{ s }}
          </a-tab-pane>
        </a-tabs>

      </a-tab-pane>
    </a-tabs>
  </div>
</template>
<script>
import { defineComponent, ref } from 'vue';
export default defineComponent({
  setup() {
    const mode = ref('top');
    const activeKey = ref('1key');
    const subActiveKey = ref('1subkey');

    const callback = val => {
      console.log('show-value.',val,activeKey);
    };

    const subCallback = val => {
      console.log('show-sub-value.',val,activeKey);
    };

    return {
      mode,
      callback,
      subCallback,
      activeKey,
      subActiveKey,
    };
  },
});
</script>